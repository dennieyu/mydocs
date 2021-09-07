AWS vs 전통적인 인프라
=====

<img title="AWS" src="./images/aws/onpremiseVsAws.png" alt="AWS" width="600px">


인프라 확장
=====
1. 인프라 확장 - `Scale Up`/`Scale Out`/`Auto Scaling`
1. 데이터베이스 확장 - `Master, Slave`/`Shading`
1. NoSQL 사용


AWS Services
=====

<img title="AWS" src="./images/aws/awsServices.png" alt="AWS" width="1000px">

- **컴퓨팅**
   - **`EC2`**: EC2 (Elastic Compute Cloud)는 AWS에서 가장 기본적이면서 널리 쓰이는 인프라로 EC2는 일종의 가상서버로 CPU와 RAM을 제공
   - **`EC2 Auto Scaling`**: 트래픽이 늘어나면 자동으로 EC2 인스턴스를 생성해 서비스를 확장하는 기능
   - **`ECS`**: ECS (Elastic Container Service)는 AWS에서 단일 또는 수천 개의 Docker 컨테이너를 쉽게 실행하고 보안을 적용할 수 있음
   - **`Lambda`** : 이벤트에 응답하여 코드를 실행하고 자동으로 기본 컴퓨팅 리소스를 관리하는 서버 없는 컴퓨팅 서비스


- **스토리지**
   - **`S3`**: S3 (Simple Storage Service)는 인터넷 스토리지 서비스로 용량에 관계 없이 파일을 저장하고 웹에서 파일에 접근
   - **`EBS`**: EBS (Elastic Block Storage)는 EC2 인스턴스에 장착하여 사용할 수 있는 가상 저장 장치로, 최대 16 TiB까지 생성이 가능
   - **`Glacier`**: 데이터 보관(Archive) 및 백업 전용 스토리지로, 요금이 매우 저렴하지만, 파일을 검색하는데 시간이 필요

   
- **데이터베이스**
   - **`RDS`**: RDS (Relational Database Service)는 관리형 관계형 데이터베이스 서비스로, 총 6개의 데이터베이스 엔진을 인스턴스 단위로 실행
   - **`Aurora`**: 클라우드를 위해 구축된 DB로 MySQL 및 PostgreSQL과 호환되며, 저렴한 비용으로 이용이 가능
   - **`DynamoDB`**: 아마존에서 개발한 NoSQL 데이터베이스를 제공하는 서비스로, 읽고 쓰는 처리 속도가 매우 빠름


- **네트워킹**
   - **`ELB`**: ELB (Elastic Load Balancing)는 부하 분산과 고가용성을 제공하는 서비스로 고가의 L4/L7 장비를 구입 없이 부하 분산 기능을 사용
   - **`VPC`**: VPC (Virtual Private Cloud)는 가상 네트워크 서비스로 사용자의 상황에 맞게 VPC를 생성해 여러가지 형태의 네트워크를 구성
   - **`CloudFront`**: 전 세계에 파일을 빠른 속도로 배포하는 CDN 서비스로 전세계 24개국에 엣지 로케이션(캐시서버)이 있음
   - **`Route 53`**: `EC2`, `ELB`, `S3`, `CloudFront`와 연동 가능한 DNS(Domain Name System) 서비스로 가용성과 확장성이 뛰어남


[EC2 Auto Scaling](https://docs.aws.amazon.com/ko_kr/autoscaling/)
-----
1. 부하에 따라 자동으로 규모 변경
1. 현재의 규모 유지
1. 시간에 따른 변경


[S3](https://aws.amazon.com/ko/s3/)
-----
1. Simple Storage Service의 약자로 클라우드 스토리지
1. 정적 웹사이트 코드 배포에 용이
1. 정적 웹사이트 호스팅에 필요한 다양한 기능 제공
1. AWS Cloudfront와 함께 사용해서 최적화 가능하고 DNS 관리도 가능
1. 파일에 인증을 붙여서 무단으로 엑세스 하지 못하도록 할 수 있음
1. REST, SOAP 인터페이스를 제공
1. 최소 1바이트에서 5TB의 데이터를 저장, 서비스


[Amazon CloudWatch](https://aws.amazon.com/ko/cloudwatch/)
-----
1. DevOps 엔지니어, 개발자, SRE(사이트 안정성 엔지니어) 및 IT 관리자를 위해 구축된 모니터링 및 관찰 기능 서비스
1. 애플리케이션을 모니터링하고, 시스템 전반의 성능 변경 사항에 대응하며, 리소스 사용률을 최적화
1. 운영 상태에 대한 통합된 보기를 확보하는 데 필요한 데이터와 실행 가능한 통찰력을 제공
1. 로그, 지표 및 이벤트 형태로 모니터링 및 운영 데이터를 수집하여 AWS와 온프레미스 서버에서 실행되는 AWS 리소스, 애플리케이션 및 서비스에 대한 통합된 보기를 제공


[Route 53](https://aws.amazon.com/ko/route53)
-----
1. 고가용성과 안정성
1. 다른 Amazon Web Services와 연동


[EKS](https://aws.amazon.com/ko/eks/)
-----
1. [**EKS**](./EKS.md) - Amazon Elastic Kubernetes Service (Amazon EKS)


[ECR](https://aws.amazon.com/ko/ecr/)
-----
1. Elastic Container Registry
1. 도커 이미지를 저장하는 private repository
1. 실제 프로덕션 환경에서는 container 기반의 배포 (ECS 등을 활용) 할 것이기 때문에 반드시 repository가 있어야 함


[ECS](https://aws.amazon.com/ko/ecs/)
-----
1. Elastic Container Service
1. 도커 컨테이너 기반으로 서비스 운용을 가능하게 해주는 간단한 서비스
1. 무중단 배포 (Rolling Update)를 제공하며 scale up 이 가능한 특징
1. 백엔드 서비스를 scale up 가능한 형태로 배포하는데 최적화
1. 수많은 도커 컨테이너 서버를 띄우고 LB가 이를 로드 밸런싱 해줌
1. fargate, ec2 모드가 있어서 docker container 리소스만 띄우거나 또는 물리적인 EC2 인스턴스를 클러스터로 구성 가능


[Amazon SNS](https://aws.amazon.com/ko/sns/)
-----
1. 애플리케이션 간(A2A) 및 애플리케이션과 사용자 간(A2P) 통신 모두를 위한 완전관리형 메시징 서비스


[Amazon SQS](https://aws.amazon.com/ko/sqs/)
-----
1. 마이크로 서비스, 분산 시스템 및 서버리스 애플리케이션을 쉽게 분리하고 확장할 수 있도록 지원하는 완전관리형 메시지 대기열 서비스


[AWS Lambda](https://aws.amazon.com/ko/lambda/)
-----
1. 서버 프로비저닝 또는 관리, 워크로드 인식 확장 로직 생성, 이벤트 통합 유지, 또는 런타임 관리 없이 코드를 실행할 수 있는 서버리스 컴퓨팅 서비스
1. 사실상 모든 유형의 애플리케이션이나 백엔드 서비스에 대한 코드를 별도의 관리 없이 실행할 수 있음


[AWS CodeDeploy](https://aws.amazon.com/ko/codedeploy/)
-----
1. Amazon EC2, AWS Fargate, AWS Lambda 및 온프레미스 서버와 같은 다양한 컴퓨팅 서비스에 대한 소프트웨어 배포를 자동화하는 완전관리형 배포 서비스
