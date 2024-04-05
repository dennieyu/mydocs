Master Data Management (MDM)
=====

- 기업 내 데이터 관리 정책과 프로세스를 관장하는 데이터 거버넌스, 그 중심에는 `MDM`(Master Data Management, 기준정보관리)이 자리하고 있다. 
- `MDM` 이란 기업의 핵심 데이터인 기준 정보를 생성하고, 이를 일관성 있게 유지하며 비즈니스 프로세스 흐름에 맞춰 정확하게 관리하기 위한 솔루션이다.

# 제품 검색

- [**skdt**](https://skdt.co.kr/data-mastering/)
- [**datastreams**](http://www.datastreams.co.kr/kor/sub/prd/governance/masterdata.asp)
- [**ibm**](https://www.ibm.com/kr-ko/analytics/master-data-management)
- [**stibosystems**](https://www.stibosystems.com/ko/what-is-master-data-management)
- [**informatica**](https://www.informatica.com/kr/products/master-data-management.html)

MSTR(MicroStrategy)
=====

MSTR(MicroStrategy)은 Self-Service, Enterprise BI, Big Data 분석을 통합 제공하는 분석 플랫폼으로 데이터 소스 관리에서부터 데이터셋 작성과 분석, 데이터 시각화, 데이터 활용까지 기업 내에서 요구하는 분석 기능들을 하나의 플랫폼에서 모두 제공

# 데이터베이스(database)

트랜잭션의 세부사항을 기록하는 것 같이 데이터를 캡쳐하고 저장하는데 사용
목적이 트랜잭션을 처리하는 것 일뿐이다.

# 데이터웨어하우스

데이터'분석'을 위해 특별히 설계된 구조
목적이 데이터분석이다.

- 수집된 대규모의 로우데이터에서 필요하는 데이터를 수정,가공해서 (정제하여) 저장한 공간,
- 그래서 DW의 데이터들은 이제 OLAP나 데이터마이닝을 통해 활용할 수 있음
- ->즉 OLAP는 DW정보를 분석하는 역할
- DW는 어떻게 데이터를 구축할 것인가에 초점,
- OLAP는 기업들이 어떻게 DW를 활용할것인가에 초점

# 데이터레이크

정형,반정형 및 비정형데이터를 비롯한 모든 가공되지 않은 다양한 종류의 데이터를 한곳에 모아둔 저장소
빅데이터를 효율적으로 분석하고 사용하고자 다양한 영역의 raw데이터를 한곳에 모아서 관리

# 데이터마트

특정 팀 또는 사업단위의 요구를 충족시킴 
규모가 더 작고, 집중적이며 사용자 커뮤니티에 가장 잘 맞는 데이터의 요약본 

# 가장 하위티어 : data

트랜잭션 시스템, RDB를 비롯한 데이터들 (주로 raw data라 불리는 것들)

# ETL과정 : Extract,Transform,Load 

ETL과정을 거쳐 스키마에 적재해둔다. 

# 중간티어1 : 데이터웨어하우스 서버 

데이터를 액세스하고 분석하는 엔진 
데이터필드 또는 문자열과 같은 레이아웃 및 유형들을 설명하는 스키마로 구성

# 중간티어2 : OLAP 서버

데이터에 엑세스하고 분석하는데 사용되는 분석엔진들 

- OLAP는 의사결정에 도움이되는 데이터분석에 관심이 있음
- 데이터의 무결성을 확보할 필요가 없다
- 이미 무결성이 확보된 데이터를 ETL작업한 상태로 저장한 DW에서 이루어지기 때문에
- 솔루션 : CRM, 데이터웨어하우스, 데이터마트, 데이터분석 및 읽기 작업에 적합하도록 가공

# 상위티어 : Frontend

실제로 데이터를 분석하고 마이닝하고 보고할때 사용하는 부분 
통계,분석,데이터마이닝,ai등을 통해 분석한 결과를 리포팅한다. 

