EKS 구성
=====

1. Bastion Host 준비
1. AWS CLI 설치
1. eksctl 설치
1. kubectl 설치
1. AWS IAM 구성
1. EKS 설치
1. EKS 삭제


Bastion Host 준비
-----

- [**참고 - AWS 가이드**](https://aws.amazon.com/ko/quickstart/architecture/linux-bastion/)
- [**참고 - 블로그**](https://blog.naver.com/pentamkt/221034903499)

- 배스천 호스트란 침입 차단 소프트웨어가 설치되어 내부와 외부 네트워크 사이에서 일종의 게이트 역할을 수행하는 호스트를 뜻함
- AWS EC2 인스턴스를 생성해서 Bastion Host 서버로 사용
   - 기본 인스턴스 생성
   - 기본 EBS 스토리지 생성
   - 인스턴스 태그 이름 생성
   - Security Group 생성
   - 인증키 생성 및 다운로드
   - Elastic IP (고정 IP) 생성
   - 고정 IP를 인스턴스와 매핑


AWS CLI 설치 (/w Bastion Host)
-----

- [**참고 - AWS 가이드**](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/install-cliv2-linux.html)
  
```
$ sudo apt-get install -y unzip
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install
$ aws --version
aws-cli/2.2.5 Python/3.8.8 Linux/4.4.0-19041-Microsoft exe/x86_64.ubuntu.20 prompt/off
```


EKS 관리툴 eksctl 설치 (/w Bastion Host)
-----

- [**참고 - AWS 가이드**](https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/eksctl.html)

```
$ curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
$ sudo mv /tmp/eksctl /usr/local/bin
$ eksctl version
0.50.0
```


k8s 관리툴 kubectl 설치 (/w Bastion Host)
-----

- [**참고 - AWS 가이드**](https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/install-kubectl.html)

```
$ curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$ mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
$ echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc
$ kubectl version --short --client
Client Version: v1.19.6-eks-49a6c0
```


AWS IAM 계정 (admin-user) 생성
-----

- root 로그인후 IAM 생성
   - 사용자이름(User name*): admin-user
   - Access Type: 프로그래밍 방식(Programmatic access) 선택
   - 기존 정책(Attach existing policies directly): administratorAccess
   - 태그 추가(Add tags (optional)) - SKIP
   - 사용자 만들기(Create User) 버튼 클릭
   - 사용자 생성되면 csv 다운로드 - 액세스ID / 시크릿엑세스키


AWS IAM 계정 (admin-user) 등록 (/w Bastion Host)
-----

- AWS IAM 계정 등록

```
$ aws configure
AWS Access Key ID [None]: AKIASJ...E37V
AWS Secret Access Key [None]: XLzhAqt...7g
Default region name [None]: ap-northeast-2
Default output format [None]: <ENTER>
```

- 확인

```
$ cd .aws/

$ cat config  
[default]
region = ap-northeast-2
 
$ cat credentials
[default]
aws_access_key_id = AKIASJ...E37V
aws_secret_access_key = XLzhAq...7g

$ aws sts get-caller-identity
{
    "UserId": "AID...KS26",
    "Account": "15..75",
    "Arn": "arn:aws:iam::158208647875:user/k8suser-console"
}
```


EKS 구성
-----

- [**참고 - AWS 가이드**](https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/getting-started-eksctl.html) 
   - EKS 요금: 시간당 0.01 USD + t3.medium 시간당 0.416 *2 USD
   - `Managed nodes – Linux` 탭 선택 후 사용 설명 확인
   - eksctl 명령을 실행해서 Amazon EKS 클러스터를 생성

```
$ eksctl create cluster \
  --name k8s-demo \
  --region ap-northeast-2 \
  --with-oidc \
  --ssh-access \
  --ssh-public-key aws-login-key \
  --nodes 3 \
  --node-type t3.medium \
  --node-volume-size=20 \
  --managed
```

- [**참고 - AWS 가이드**](https://aws.amazon.com/ko/about-aws/whats-new/2021/02/amazon-eks-clusters-support-user-authentication-oidc-compatible-identity-providers/)
  - Amazon EKS 에서 `OpenID Connect (OIDC)` 호환 자격 증명 공급자를 Kubernetes 클러스터에 대한 사용자 인증 옵션으로 사용할 수 있다. 
  - `OIDC` 인증을 사용하면 직원 계정의 생성, 활성화 및 비활성화에 대한 조직의 표준 절차를 사용하여 EKS 클러스터에 대한 사용자 액세스를 관리할 수 있다. 

- `aws-login-key`는 인스턴스 생성 시 인증키 생성했었음

- `CloudFormation`으로 생성되기 때문에 aws에서 cloudformation 검색 후 확인. 생성되는 시간이 20분 정도 걸림

```
eksctl version 0.50.0
using region ap-northeast-2
setting availability zones to [ap-northeast-2a ap-northeast-2b ap-northeast-2c]
...
```


EKS 구성 결과 확인 및 CLI 명령어 자동완성 기능을 추가
-----

- kubectl 명령으로 설치 결과 확인

```
$ kubectl get nodes
NAME                                                STATUS   ROLES    AGE   VERSION
ip-192-168-38-198.ap-northeast-2.compute.internal   Ready    <none>   28m   v1.19.6-eks-49a6c0
ip-192-168-4-22.ap-northeast-2.compute.internal     Ready    <none>   28m   v1.19.6-eks-49a6c0
ip-192-168-82-229.ap-northeast-2.compute.internal   Ready    <none>   28m   v1.19.6-eks-49a6c0
```

- CLI 명령어 완성기능 추가

```
$ source <(kubectl completion bash)
$ echo "source <(kubectl completion bash)" >> ~/.bashrc
```


간단한 실행 실습
-----

- 워커 노드 정보 보기

```
$ kubectl get nodes -o wide
```

- Pod 배포 테스트. nginx 컨테이너 5개 실행하고 결과 확인

```
$ kubectl create deployment webtest --image=nginx:1.14 --port=80  --replicas=5
$ kubectl get  pods -o wide
NAME                      READY   STATUS    RESTARTS   AGE   IP               NODE                                               NOMINATED NODE   READINESS GATES
webtest-fdf54587f-8mfrz   1/1     Running   0          28s   192.168.10.139   ip-192-168-2-91.ap-northeast-2.compute.internal    <none>           <none>
webtest-fdf54587f-d4pjc   1/1     Running   0          28s   192.168.39.104   ip-192-168-56-22.ap-northeast-2.compute.internal   <none>           <none>
webtest-fdf54587f-dqg55   1/1     Running   0          28s   192.168.13.27    ip-192-168-2-91.ap-northeast-2.compute.internal    <none>           <none>
webtest-fdf54587f-hs8zd   1/1     Running   0          28s   192.168.77.185   ip-192-168-70-30.ap-northeast-2.compute.internal   <none>           <none>
webtest-fdf54587f-pn549   1/1     Running   0          28s   192.168.83.249   ip-192-168-70-30.ap-northeast-2.compute.internal   <none>           <none>
```

- nginx 웹서버에 클라이언트 접속 가능하도록 구성하고 간단히 테스트

```
$ kubectl expose deployment webtest --port=80 --type=LoadBalancer
$ kubectl get services
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP                                                                    PORT(S)        AGE
kubernetes   ClusterIP      10.100.0.1      <none>                                                                         443/TCP        33h
webtest      LoadBalancer   10.100.222.89   ab5190278c9ac491cb45a4bc42a6d689-1608401336.ap-northeast-2.elb.amazonaws.com   80:30331/TCP   31s
```

- 1분정도 후에 웹브라우저를 통해 웹서버 연결되는지 확인
   - http://ab5190278c9ac491cb45a4bc42a6d689-1608401336.ap-northeast-2.elb.amazonaws.com


EKS 삭제
-----

- 더이상 EKS 사용하지 않는다면 아래 명령으로 삭제 (삭제하지 않고 두면 EKS, EC2 모두 과금됨)

```
$ eksctl delete cluster --name k8s-demo
```


EFS 구성
=====

1. Amazon EFS 생성
1. Node와 연결 TEST
1. efs dynamic provisioner 배포
1. PVC 생성


Amazon EFS 생성
-----

- [**참고 - AWS 가이드**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEFS.html)

- Amazon EFS 생성
   - **Step1** File system settings
   - **Step2** Network access
   - **Step3** File system policy
   - **Step4** Review and create

Node와 연결 TEST
-----

- EFS 마운트
   - node1, node2, node3 

```
$ mkdir /shared-data
$ mount -t nfs4 파일시스템ID.efs.ap-northeast-2.amazoneaws.com:/ /shared-data
$ mount | tail -1
```

efs dynamic provisioner 배포
-----

```
$ pwd
/home/ubuntu/aws-efs-provisioner

$ ls
configmap.yaml    rbac.yaml    efs-provisioner-deploy.yaml    storage-class.yaml

$ kubectl apply -f storage-class.yaml -f rbac.yaml -f efs-provisioner-deploy.yaml -f configmap.yaml
```

PVC 생성
-----

```
$ ls
configmap.yaml    rbac.yaml    efs-provisioner-deploy.yaml    storage-class.yaml    my-pvc.yaml

$ kubectl apply -f my-pvc.yaml
```
