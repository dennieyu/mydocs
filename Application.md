아키텍쳐
=====


## Application 아키텍쳐

- **OCP와 전략 패턴**

<img title="application" src="./images/aa/ocp_strategy-pattern.png" alt="application" width="760px">

- **MVC 패턴**

<img title="application" src="./images/aa/mvc_pattern.png" alt="application" width="560px">

- **메모리 캐시**

<img title="application" src="./images/aa/cache.png" alt="application" width="600px">

- **어플리케이션 캐시**

<img title="application" src="./images/aa/application_cache.png" alt="application" width="320px">

- **레벨2 캐시**

<img title="application" src="./images/aa/level_2_cache.png" alt="application" width="400px">

- **MVVM**
   
   - 불변 개체와 Rx를 활용해 상태를 관리하는 응용프로그램 아키텍쳐
   
   - MVVM 응용프로그램
   
   <img title="application" src="./images/aa/mvvm-pattern.png" alt="application" width="700px">
   
   - MVVM 서비스 클라이언트 응용프로그램
   <img title="application" src="./images/aa/service-client-app-with-mvvm.png" alt="application" width="700px">

- [**Reactive Programming**](./RxJS_202101.pdf)

   - **이벤트 스트림**을 **`Observable`** 이라는 객체로 표현한 후 **비동기 이벤트 기반**의 프로그램을 작성
   
   <img title="application" src="./images/aa/reactive-programming.png" alt="application" width="700px">


## Software 아키텍쳐


- **Proxy**

   - Forward Proxy: 내부 인트라넷에서 인터네상에 있는 서버에 요청할 때 먼저 프록시 서버를 호출하게 되는데 이런 방식이 포워드 프록시
   - Reverse Proxy: 내부 인트라넷에 있는 서버를 호출하기 위해서 인터넷 망에 있는 클라이언트가 리버스 프록시 서버에 요청하여 응답을 받는 방식
      - 특징: 보안, 성능, 트래픽 분산

- **이벤트 소싱**

<img title="application" src="./images/aa/event-sourcing-pattern.png" alt="application" width="700px">

- **CQRS**

<img title="application" src="./images/aa/cqrs_and_event-sourcing.png" alt="application" width="900px">

- **MSA**

   - [**마이크로서비스**](./마이크로서비스.md)

   - [**서비스메쉬**](./이스티오.md)
