## Database POOL
### POOL이란?
'컴퓨터 과학에서 풀은 사용할 때 획득한 메모리와 나중에 해제되는 메모리가 아닌, 사용할 준비가 된 메모리에 유지되는 리소스 모음'을 의미

뇌피셜 : 수영장과 같이 데이터가 모아있는 어떠한 저장소, 데이터에 접근해서 끄집어 냈다가 놓을 수 있는 곳이지 않을까

* 자바에서 DB에 직접 연결해서 처리하는 경우 JDBC Driver를 로드하고 커넥션 객체를 받아와야 한다. 그러면 매번 사용자가 요청을 할 때마다 드라이버를 로드하고 커넥션 객체를 생성하여 연결하고 종료하기 때문에 매우 비효율적이다. 이런 문제를 해결하기 위해서 커넥션 풀을 사용한다.

* 특수한 풀로 connection pool, thread pool 및 memory pool이 존재한다.


![connection_pool.png](connection_pool.png)


### DB POOL의 장점

Connection pool은 매번 새로운 접속을 통해서 쿼리를 통해 DB에서 정보를 가지고 온다. 이는 컴터에게 너무나 큰 무리를 주기 때문에 해당 서버의 cpu점유율을 높이는 직접적인 원인이 될수있다. 그래서 우리는 DB를 제어하기전에 "사용자 지정 갯수만큼 커넥션을 만들어놓고 pool에 넣어놓았다가 필요할때마다 갔다가 쓰고 사용을 다하면 다시 pool에 넣어놓고 사용하는 식"으로 시스템을 효율적으로 운영한다.









### References
[블로그 레퍼런스1](https://lovestudycom.tistory.com/entry/DB-POOL-%EC%9D%B4%EB%9E%80)
[블로그 레퍼런스2](https://steady-coding.tistory.com/564)
[블로그 레퍼런스3](https://velog.io/@ohdowon064/CS-%ED%92%80Pool%EC%9D%B4%EB%9E%80)
[블로그 레퍼런스4](https://lovestudycom.tistory.com/entry/DB-POOL-%EC%9D%B4%EB%9E%80)
