@Transactional
=====


problem
-----
1. `Dirty Read`
1. `Non-Repeatable Read`
1. `Phantom Read`


isolation
-----
- **DEFAULT**
   - **DB의 Isolation Level을 따름**
- **READ_UNCOMMITTED (level 0)**
   - 커밋되지 않는(트랜잭션 처리중인) 데이터에 대한 읽기를 허용
   - 즉 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 B라는 아직 완료되지 않은(Uncommitted 혹은 Dirty) 데이터 B를 읽을 수 있다.
   - `Dirty Read` 발생
- **READ_COMMITTED (level 1)**
   - 트랜잭션이 커밋 된 확정 데이터만 읽기 허용
   - 어떠한 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 해당 데이터에 접근할 수 없다.
   - `Dirty Read` 방지
- **REPEATABLE_READ (level 2)**
   - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능하다.
   - 선행 트랜잭션이 읽은 데이터는 트랜잭션이 종료될 때까지 후행 트랜잭션이 갱신하거나 삭제가 불가능 하기때문에 같은 데이터를 두 번 쿼리했을 때 일관성 있는 결과를 리턴한다.
   - `Non-Repeatable Read` 방지
- **SERIALIZABLE (level 3)**
   - 데이터의 일관성 및 동시성을 위해 MVCC(Multi Version Concurrency Control)을 사용하지 않음
   - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능하다.
   - `Phantom Read` 방지
- **격리 수준이 올라갈 수록 성능 저하의 우려가 있음**


propagation
-----
- **REQUIRED**
   - 디폴트 속성, 부모 트랜잭션 내에서 실행하며 부모 트랜잭션이 없을 경우 새로운 트랜잭션을 생성한다.
- **SUPPORTS
   - 이미 시작된 트랜잭션이 있으면 참여하고 그렇지 않으면 트랜잭션 없이 진행하게 만든다. 
- **REQUIRES_NEW**
   - 부모 트랜잭션을 무시하고 무조건 새로운 트랜잭션이 생성
- **MANDATORY**
   - REQUIRED와 비슷하게 이미 시작된 트랜잭션이 있으면 참여한다.
   - 반면에 트랜잭션이 시작된 것이 없으면 새로 시작하는 대신 예외를 발생시킨다.
   - 혼자서는 독립적으로 트랜잭션을 진행하면 안 되는 경우에 사용한다.
- **REQUIRES_NEW**
   - 항상 새로운 트랜잭션을 시작한다.
   - 이미 진행 중인 트랜잭션이 있으면 트랜잭션을 잠시 보류시킨다.
- **NOT_SUPPORTED**
   - 트랜잭션을 사용하지 않게 한다.
   - 이미 진행 중인 트랜잭션이 있으면 보류시킨다.
- **NEVER**
   - 트랜잭션을 사용하지 않도록 강제한다.
   - 이미 진행 중인 트랜잭션도 존재하면 안된다 있다면 예외를 발생시킨다.
- **NESTED**
   - 이미 진행중인 트랜잭션이 있으면 중첩 트랜잭션을 시작한다.
   - 중첩 트랜잭션은 트랜잭션 안에 다시 트랜잭션을 만드는 것이다.


예제
-----
- REQUIRES 에서 REQUIRES_NEW 으로 수정

```
# 변경 전
begin  
delete < for 반복문
commit

# 변경 후
for
 begin
     delete
 commit
for end  
```
