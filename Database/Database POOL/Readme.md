## Database POOL
### POOL이란?
'컴퓨터 과학에서 풀은 사용할 때 획득한 메모리와 나중에 해제되는 메모리가 아닌, 사용할 준비가 된 메모리에 유지되는 리소스 모음'을 의미

뇌피셜 : 수영장과 같이 데이터가 모아있는 어떠한 저장소, 데이터에 접근해서 끄집어 냈다가 놓을 수 있는 곳이지 않을까

* 자바에서 DB에 직접 연결해서 처리하는 경우 JDBC Driver를 로드하고 커넥션 객체를 받아와야 한다. 그러면 매번 사용자가 요청을 할 때마다 드라이버를 로드하고 커넥션 객체를 생성하여 연결하고 종료하기 때문에 매우 비효율적이다. 이런 문제를 해결하기 위해서 커넥션 풀을 사용한다.

* 특수한 풀로 connection pool, thread pool 및 memory pool이 존재한다.


![connection_pool.png](connection_pool.png)


### DBCP 의 장점

Connection pool은 매번 새로운 접속을 통해서 쿼리를 통해 DB에서 정보를 가지고 온다. 
이 때 클라이언트와 서버 사이드인 웹 어플리케이션에서, 사용자의 요청에 따라 Connection이 생성된다면 수 많은 사용자가 요청을 했을 때 서버에 과부하가 걸리게 된다
이는 컴터에게 너무나 큰 무리를 주기 때문에 해당 서버의 cpu점유율을 높이는 직접적인 원인이 될수있다. 

이러한 상황을 예방하기 위해 미리 일정 갯수의 Connection을 만들어 Pool에 저장을 하고, 사용자의 요청이 발생하면 사용자 지정 갯수만큼 Connection을 제공하고 사용자와의 연결이 종료된다면 Pool에 다시 반환하여 보관을 해서 cpu의 점유율을 줄인다

* 서버 다운의 비용적 문제를 해결함
* 클라이언트가 사용을 마친 후에는 Pool에 다시 Connection 객체를 반환하기 때문에 데이터베이스 접근 요청이 존재하더라도 새로운 Connection 객체를 생성할 필요가 없음









### References
[블로그 레퍼런스1](https://lovestudycom.tistory.com/entry/DB-POOL-%EC%9D%B4%EB%9E%80)
[블로그 레퍼런스2](https://steady-coding.tistory.com/564)
[블로그 레퍼런스3](https://velog.io/@ohdowon064/CS-%ED%92%80Pool%EC%9D%B4%EB%9E%80)
[블로그 레퍼런스4](https://lovestudycom.tistory.com/entry/DB-POOL-%EC%9D%B4%EB%9E%80)
[블로그 레퍼런스5](https://zzang9ha.tistory.com/376)
