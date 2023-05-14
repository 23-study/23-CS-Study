## **Replication**

- 정의) 실시간 복제본 데이터베이스 서버를 운용하는 것
    - 두 개 이상의 DBMS 시스템을 Master / Slave(Replica)로 나눠서 동일한 데이터를 저장함
    - Master Node는 쓰기 작업만을 처리하고, Slave Node는 읽기 작업만을 처리함
    - 비동기 방식으로 노드들 간의 데이터를 동기화함
- 등장 배경)
    - 하나의 서버와 하나의 Database를 뒀더니 사용자가 많아졌을 때 Database가 많은 Query를 처리하기 힘든 상황이 옴.
    - 이때 Query의 대부분을 차지하는 Select를 어느 정도 해결하기 위해 등장한 방법이 Replication임
    - Replication 적용 전 </br>
        <img src="https://github.com/23-study/23-CS-Study/blob/ChooSeoyeon/Database/Replication/Replication%20%EC%A0%81%EC%9A%A9%20%EC%A0%84.png?raw=true">
    - Replication 적용 후 </br>
        <img src="https://github.com/23-study/23-CS-Study/blob/ChooSeoyeon/Database/Replication/Replication%20%EC%A0%81%EC%9A%A9%20%ED%9B%84.png?raw=true">

- 방법)
    1. 어플리케이션이 데이터베이스에 SQL 명령을 보내 데이터 삽입/변경/삭제 요청보냄
    2. Master가 요청 받아 `binary log` 생성하여 Slave 서버로 전달함
    3. Master로부터 전달받은 `binary log`를 데이터로 반영함
    - 데이터 복사하는 방법 구체적으로 </br>
        <img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0b9c1e32-06fe-484c-ad42-2c22813bcfa1%2FUntitled.png?table=block&id=a4d0fa62-c51e-4da1-9dc5-f36b03760ff2&spaceId=a98aa686-1767-4142-a9a2-f7303fcfa347&width=2000&userId=d30f258c-d9aa-4582-87a1-adc478dcd1b6&cache=v2" width="350px">
        
        1. `Master`가 `binary log`를 만들어 이벤트를 기록한다.
        2. 각 `Slave`는 어떤 이벤트까지 저장되어 있는지를 기억하고 있다.
        3. `Slave`의 `IO thread`를 통해서 `Master`에 이벤트를 요청하고 받는다.
        4. `Master`는 이벤트를 요청받으면 `binlog dump thread`를 통해서 클라이언트에게 이벤트를 전송한다.
        5. `IO thread`는 전송받은 덤프 로그를 이용하여 `relay log`를 만든다.
        6. `SQL thread`는 `relay log`를 읽어서 이벤트를 다시 실행하여 `Slave`에 데이터를 복사한다.
- 장점) 데이터 백업, DBMS 부하 분산
    - Slave가 Master와 거의 실시간으로 동일한 데이터를 갖고 있어, 장애 복구 시 데이터 손실 최소화됨 (데이터 안정성)
        - Slave 서버를 Master 서버로 승격시켜 기존 Master 대체하는 방식으로 복구 진행됨
    - 비동기 방식으로 운영되어 지연 시간이 거의 없다.
    - DB 요청의 60~80% 정도가 읽기 작업이기 때문에 Replication만으로도 충분히 성능을 높일 수 있다.
- 단점)
    - 노드들 간의 데이터 동기화가 보장되지 않아 일관성있는 데이터를 얻지 못할 수 있다.
    - Master 노드가 다운되면 복구 및 대처가 까다롭다.

## Replication vs Clustering

- Replication
    - 정의) 여러 개의 DB를 수직적(Master, Slave)인 구조로 구축하는 방식
    - 특징) 비동기 방식으로 노드들 간에 데이터 동기화
    - 장점) 비동기 방식으로 데이터가 동기화되어 지연시간이 거의 없음
    - 단점) 노드들 간의 데이터가 동기화되지 않아 일관성 있는 데이터 얻지 못할 수 있음
- Clustering
    - 정의) 여러 개의 DB를 수평적인 구조로 구축하는 방식
    - 특징) 동기 방식으로 노드들 간에 데이터 동기화
    - 장점) 1개의 노드가 죽어도 다른 노드가 살아 있어 시스템을 장애 없이 운영할 수 있음
    - 단점) 여러 노드들 간의 데이터를 동기화하는 시간이 필요하므로 Replication에 비해 쓰기 성능이 떨어짐

## AWS에서의 Database Replication

- AWS의 RDS는 특정 데이터베이스 타입에 대해 Replication 기능을 지원함
- 복제 서버인 Replica는 읽기 전용임
- Postgresql, Mysql, MaraiDB에 대해 지원함

## Scale-out vs Scale-up

결론만 먼저 말씀드리자면, Replication은 Scale-out 기법 중 하나입니다. </br>
<img src="https://github.com/23-study/23-CS-Study/blob/ChooSeoyeon/Database/Replication/Scale%20up%20Scale%20out.png?raw=true" width="400px">

- Scale-out
    - 정의) ‘스케일 아웃’이란 접속된 서버를 여러 대 추가하여 처리 능력을 향상하는 방법임
    - 특징)
        - 수평 스케일로 불리기도 함
        - 예를 들어, 하나의 처리 능력을 가진 서버에 동일한 서버 6대를 더 추가하여, 총 7의 처리 능력을 만드는 것임
    - 기법)
        - Replication </br>
            <img src="https://github.com/23-study/23-CS-Study/blob/ChooSeoyeon/Database/Replication/Scale%20out.png?raw=true" width="400px">
        - Sharding </br>
            <img src="https://github.com/23-study/23-CS-Study/blob/ChooSeoyeon/Database/Replication/Scale%20up.png?raw=true" width="400px">
- Scale-up
    - 정의) ‘스케일 업’은 서버에 CPU나 RAM 등을 추가하거나 고성능의 부품, 서버로 교환하는 방법을 의미함
    - 특징)
        - 수직 스케일로 불리기도 함
        - 예를 들어, 하나의 처리 능력을 가진 서버 한 대를 7의 처리 능력을 가진 서버로 그 자체의 처리능력을 향상시키는 것임

- 참고)
    - [https://nesoy.github.io/articles/2018-02/Database-Replication](https://nesoy.github.io/articles/2018-02/Database-Replication)
    - [https://www.coovil.net/db-replication/](https://www.coovil.net/db-replication/)
    - [https://mangkyu.tistory.com/97](https://mangkyu.tistory.com/97)
    - [https://velog.io/@zpswl45/DB-Replication-개념-정리](https://velog.io/@zpswl45/DB-Replication-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)
    - [https://theheydaze.tistory.com/593](https://theheydaze.tistory.com/593)
    - [https://tecoble.techcourse.co.kr/post/2021-09-18-replication_clustering/](https://tecoble.techcourse.co.kr/post/2021-09-18-replication_clustering/)
    - [https://server-talk.tistory.com/240](https://server-talk.tistory.com/240)
    - 구성 방법 [https://www.didim365.com/blog/20200424b-blog/](https://www.didim365.com/blog/20200424b-blog/)
    - 바이너리 로그 [https://blog.seulgi.kim/2015/05/how-mysql-replication.html](https://blog.seulgi.kim/2015/05/how-mysql-replication.html)
    - 공식문서 [https://dev.mysql.com/doc/refman/5.7/en/replication.html](https://dev.mysql.com/doc/refman/5.7/en/replication.html)
    - Scale out [https://prezi.com/wwjihh6qsnwb/database-scale-out/](https://prezi.com/wwjihh6qsnwb/database-scale-out/)
