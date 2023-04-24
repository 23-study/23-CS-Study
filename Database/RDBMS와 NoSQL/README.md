# RDBMS와 NoSQL

### 차이점
|  | RDBMS | NoSQL |
| --- | --- | --- |
| 개발 이력 | 데이터 중복 감소에 중점을 두고 1970년대에 개발됨 | 2000년대 후반에 확장에 중점을 두고 애자일 및 DevOps 방식으로 구동되는 신속한 애플리케이션 변경을 허용하도록 개발됨. |
| 데이터 모델 | 스키마 있음 (Schema-based) | 스키마 없음 (Schema-less) |
| 데이터 저장 | 행(Row)과 열(Column)이 고정된 테이블 | 문서: JSON 문서/키-값: 키-값 쌍/와이드 열: 행과 동적 열이 있는 테이블/그래프: 노드 및 가장자리 |
| 예 | Oracle, MySQL, Microsoft SQL Server 및 PostgreSQL | 문서: MongoDB 및 CouchDB/키-값: Redis 및 DynamoDB/와이드 컬럼: Cassandra 및 HBase/그래프: Neo4j 및 Amazon Neptune |
| 유연성 | X | O |
| 확장성 | X (수직적 확장이 쉬움) | O (수평적 확장이 쉬움) |
| 일관성/트랜잭션 | O (ACID 제공) | X |
| 쿼리 언어 | SQL | 제품마다 지원하는 언어가 다름 |
| 클라우드 | 클라우드 환경에 적합하지 않을 수있음 | 클라우드 환경에 적합함 |
| 데이터 크기 | 대용량 데이터 처리가 어려울 수있음 | 대용량 데이터 처리가 용이함 |
| 데이터-객체 매핑 | ORM(객체 관계형 매핑) 필요 | 대부분의 경우 ORM이 필요하지 않음. MongoDB 문서는 가장 널리 사용되는 프로그래밍 언어의 데이터 구조에 직접 매핑됨. |
| 조인 | 일반적으로 필수 | 일반적으로 필요하지 않음 |



### 용어

| SQL | MongoDB |
| --- | --- |
| 테이블 | 컬렉션 |
| 행 | 도큐먼트 |
| 열 | 필드 |
| 테이블 조인 | 임베디드 도큐먼트 & 링킹 |
- 참고
    - [https://invicredible.tistory.com/entry/NoSQL과-RDBMS-비교](https://invicredible.tistory.com/entry/NoSQL%EA%B3%BC-RDBMS-%EB%B9%84%EA%B5%90)
    - [https://velog.io/@janeljs/RDBMS-NoSQL](https://velog.io/@janeljs/RDBMS-NoSQL)
    - [https://bottleh.netlify.app/backend/RDBMS vs NoSQL/](https://bottleh.netlify.app/backend/RDBMS%20vs%20NoSQL/)
    - [https://dataonair.or.kr/db-tech-reference/d-lounge/technical-data/?mod=document&uid=236128](https://dataonair.or.kr/db-tech-reference/d-lounge/technical-data/?mod=document&uid=236128)
