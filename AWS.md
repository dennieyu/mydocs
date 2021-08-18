AWS vs 전통적인 인프라
=====

<img title="AWS" src="./images/aws/onpremiseVsAws.png" alt="AWS" width="600px">


AWS Services
=====

<img title="AWS" src="./images/aws/awsServices.png" alt="AWS" width="1000px">

- **컴퓨팅**
   - **`EC2`**: EC2 (Elastic Compute Cloud)는 AWS에서 가장 기본적이면서 널리 쓰이는 인프라로 EC2는 일종의 가상서버로 CPU와 RAM을 제공
   - **`ECS`**: ECS (Elastic Container Service)는 AWS에서 단일 또는 수천 개의 Docker 컨테이너를 쉽게 실행하고 보안을 적용할 수 있음
   - **`EC2 Auto Scaling`**: 트래픽이 늘어나면 자동으로 EC2 인스턴스를 생성해 서비스를 확장하는 기능
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
   - **`VPC`**: VPC (Virtual Private Cloud)는 가상 네트워크 서비스로 사용자의 상황에 맞게 VPC를 생성해 여러가지 형태의 네트워크를 구성
   - **`CloudFront`**: 전 세계에 파일을 빠른 속도로 배포하는 CDN 서비스로 전세계 24개국에 엣지 로케이션(캐시서버)이 있음
   - **`Route 53`**: EC2, ELB, S3, CloudFront와 연동 가능한 DNS(Domain Name System) 서비스로 가용성과 확장성이 뛰어남
   - **`ELB`**: ELB (Elastic Load Balancing)는 부하 분산과 고가용성을 제공하는 서비스로 고가의 L4/L7 장비를 구입 없이 부하 분산 기능을 사용


EKS
-----
1. [**EKS**](./EKS.md) - Amazon Elastic Kubernetes Service (Amazon EKS)


S3
-----
1. Simple Storage Service의 약자로 클라우드 스토리지
1. 정적 웹사이트 코드 배포에 용이
1. 정적 웹사이트 호스팅에 필요한 다양한 기능 제공
1. AWS Cloudfront와 함께 사용해서 최적화 가능하고 DNS 관리도 가능


ECR
-----
1. Elastic Container Registry
1. 도커 이미지를 저장하는 private repository
1. 실제 프로덕션 환경에서는 container 기반의 배포 (ECS 등을 활용) 할 것이기 때문에 반드시 repository가 있어야 함


ECS
-----
1. Elastic Container Service
1. 도커 컨테이너 기반으로 서비스 운용을 가능하게 해주는 간단한 서비스
1. 무중단 배포 (Rolling Update)를 제공하며 scale up 이 가능한 특징
1. 백엔드 서비스를 scale up 가능한 형태로 배포하는데 최적화
1. 수많은 도커 컨테이너 서버를 띄우고 LB가 이를 로드 밸런싱 해줌
1. fargate, ec2 모드가 있어서 docker container 리소스만 띄우거나 또는 물리적인 EC2 인스턴스를 클러스터로 구성 가능

