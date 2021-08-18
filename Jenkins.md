jenkins CI/CD 구성
=====

참조 - [**영상/이남훈님**](https://www.youtube.com/watch?v=JPDKLgX5bRg)


jenkins 설치
-----
  
```
$ yum update -y

# 패키지 추가
$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins.io/redhat/jenkins.repo
$ sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key

# java, jenkins, docker, git 설치
$ sudo yum install -y java-1.8.0-openjdk jenkins docker git

# java 8 로 설정
$ alternatives --config java
```


jenkins 사용자에게 docker 권한 부여
-----

```
$ sudo usermod -aG docker jenkins
```


jenkins 실행
-----

```
$ sudo service jenkins start
```


docker 실행
-----

```
$ sudo service docker start
```


jenkins 구동
-----

- jenkins 첫 페이지
   - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` 명령으로 나타난 패스워드를 복사하여 입력

- 초기 plugin 설치
   - Install suggested plugins를 권장

- 초기 관리자 생성
   - 이 과정을 마치면 jenkins 대시보드까지 들어올 수 있음


set jenkins credential for git
-----

- github에서 `access token` 생성
   - 프로필 > settings > developer settings > personal access tokens > generated new token 클릭
   - repo에 관한 권한만 주고 token 생성

- git credential 등록
   - jenkins 관리 > manage credentials > jenkins > global credentials > add credential
      - Kind: Username with password
      - Username: (github id)
      - Password: (github 에서 생성한 `access token` 입력)
      - ID: (임의로 유일하게 작성)
      ※ jenkins에서 git에 접근하기 위한 credential한 id (추천 - gitCredentialTokenForJenkins을 줄여서 gctfj)


set jenkins credential for AWS EC2
-----

- root 로그인 후 IAM 생성
   - 사용자이름(User name*): jenkins-user
   - Access Type: 프로그래밍 방식(Programmatic access) 선택
   - 기존 정책(Attach existing policies directly): administratorAccess
   - 태그 추가(Add tags (optional)) - SKIP
   - 사용자 만들기(Create User) 버튼 클릭
   - 사용자 생성되면 csv 다운로드 - `엑세스키ID` / `시크릿엑세스키`

- IAM 에서 생성한 key를 jenkins 유저에 등록
   - jenkins 관리 > manage credentials > jenkins > global credentials > add credential
      - Kind: Secret text
      - Secret: (`엑세스키ID` or `시크릿엑세스키`)
      - ID: (awsAccessKeyId or awsSecretAccessKey)


create AWS s3 bucket
-----

- AWS 서비스에서 s3 검색
- 버킷 생성


install docker plugin
-----

- jenkins 관리 > 플러그인 관리 > 설치 가능 > docker 검색
- 검색된 plugin 중에서 docker pipeline, docker를 설치


jenkinsfile 작성
-----
```
pipeline {
    // 스테이지 별로 다른 거
    agent any

    triggers {
        pollSCM('*/3 * * * *')
    }

    environment {
        AWS_ACCESS_KEY_ID = credentials('awsAccessKeyId')
        AWS_SECRET_ACCESS_KEY = credentials('awsSecretAccessKey')
        AWS_DEFAULT_REGION = 'ap-northeast-2'
        HOME = '.' // Avoid npm root owned
    }

    stages {
        // 레포지토리를 다운로드 받음
        stage('Prepare') {
            agent any

            steps {
                echo 'Git Repository'

                git url: 'https://github.com/user_account/temp.git',
                    branch: 'master',
                    credentialsId: 'jenkinsgit'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo 'Successfully pulled from git repository'
                }

                always {
                    echo 'I tried...'
                }

                cleanup {
                    echo 'After all other post conditions'
                }
            }
        }
        
        stage('Only for production') {
            when {
                branch 'production'
                environment name: 'APP_ENV', value: 'prod'
                anyOf {
                    environment name: 'DEPLOY_TO', value: 'production'
                    environment name: 'DEPLOY_TO', value: 'staging'
                }
            }
        }

        // AWS s3 에 파일을 올림
        stage('Deploy Frontend') {
            steps {
                echo 'Deploying Frontend'
                // 프론트엔드 디렉토리의 정적파일들을 S3 에 올림, 이 전에 반드시 EC2 instance profile 을 등록해야함.
                dir ('./website') {
                    sh '''
                    aws s3 sync ./ s3://user_s3_name
                    '''
                }
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo 'Successfully deployed to s3 repository'

                    mail to: 'user_account@gmail.com',
                         subject: 'Deploy Frontend Success',
                         body: 'Successfully deployed frontend!'
                }

                failure {
                    echo 'I failed :('

                    mail to: 'user_account@gmail.com',
                         subject: 'Failed Pipelinee',
                         body: 'Something is wrong with deploy frontend'
                }
            }
        }

        stage('Lint Backend') {
            // Docker plugin and Docker Pipeline 두개를 깔아야 사용가능!
            agent {
                docker {
                    image 'node:latest'
                }
            }

            steps {
                dir ('./server') {
                    sh '''
                    npm install&&
                    npm run lint
                    '''
                }
            }
        }

        stage('Test Backend') {
            agent {
                docker {
                    image 'node:latest'
                }
            }
            steps {
                echo 'Test Backend'

                dir ('./server') {
                    sh '''
                    npm install
                    npm run test
                    '''
                }
            }
        }

        stage('Bulid Backend') {
            agent any
            steps {
                echo 'Build Backend'

                dir ('./server') {
                    sh """
                    docker build . -t server --build-arg env=${PROD}
                    """
                }
            }

            post {
                failure {
                    error 'This pipeline stops here...'
                }
            }
        }

        stage('Deploy Backend') {
            agent any

            steps {
                echo 'Deploy Backend'

                dir ('./server') {
                    sh '''
                    docker rm -f $(docker ps -aq)
                    docker run -p 80:80 -d server
                    '''
                }
            }

            post {
                success {
                    mail to: 'user_account@gmail.com',
                         subject: 'Deploy Success',
                         body: 'Successfully deployed!'
                }
            }
        }
    }
}
```


jenkins item 만들기
-----

- Dashboard > 새로운 Item > myproject
- pipeline으로 생성
   - jenkinsfile(pipeline script)도 git에서 받아와서 관리되도록 할 수도 있고, pipeline script를 직접 작성 할 수도 있음


jenkinsfile에 사용될 환경변수 설정
-----

- jenkins 관리 > 시스템 설정 > Global properties에서 key/value 형태로 환경변수를 작성


build 실행
-----

- jenkinsfile에 적힌 순서대로 파이프라인이 동작하는지 확인
- 오류가 나면 로그를 통해 모든 이슈 확인 가능
- 정상적으로 배포가 완료되면 S3에 최종적으로 index.html가 올라간 것을 확인


실제 사용 사례
-----

- 배포 자동화를 위해 laaC 툴인 Terraform 사용


참고 강좌
=====

- [**Jenkins를 활용한 CI/CD/Tacademy**](https://tacademy.skplanet.com/live/player/onlineLectureDetail.action?seq=190)
