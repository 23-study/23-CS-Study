# Statement와 PreparedStatement

### SQL 실행 단계

> 1. 쿼리 문장 분석
> 2. 컴파일
> 3. 실행

<br>

## 💡 Statement

```JAVA
String sqlstr = "SELECT name, memo FROM TABLE WHERE name =" + num
Statement stmt = conn.createStatement();
ResultSet rst = stmt.executeQuery(sqlstr);
```

<br>

- 쿼리문을 실행할 때마다 위 SQL 실행 단계의 1 ~ 3 단계를 반복
- 실행되는 SQL 문 확인 가능
- SQL 문을 수행하는 과정에서 매번 컴파일을 하기 때문에 성능상 이슈가 있다

<br>

### 장점과 단점

**장점**<br>
- 테이블, 컬럼에 대한 동적 쿼리 작성이 가능
  - DDL(CREATE, ALTER, DROP) 작성에 적합
- 실행되는 SQL 문을 확인 가능하므로 쿼리 분석이 쉽다

**단점**<br>
- SQL 문 수행할 때마다 컴파일을 하므로 쿼리 처리 비용이 더 들게 된다
- SQL 문을 실행할 때 쿼리를 문자열로 동적으로 구성하고 데이터베이스에 전송해 실행하기 때문에 SQL Injection 에 취약하다

<br>

## 💡 PreparedStatement

```JAVA
String sqlstr = "SELECT name, memo FROM TABLE WHERE num = ?"
PreparedStatement stmt = conn.preparedStatement();
stmt.setInt(1, num);
ResultSet rst = stmt.executeQuery(sqlstr);
```

<br>

- 쿼리를 수행할 때, 처음 한 번만 위 SQL 실행 단계의 1 ~ 3 단계를 거치고, 그 후 캐시에 담아 재사용
- 컴파일이 미리 되어있어 Statement 에 비해 성능상 이점이 있음
- "?" 부분에만 변화를 주어 쿼리문을 실행하므로 실행되는 쿼리를 파악하기 어려움

<br>

### 장점과 단점

**장점**<br>
- SQL 문을 미리 컴파일하여 재사용하기 때문에 SQL 처리가 빠르다
- SQL 쿼리와 입력값이 분리되어 쿼리를 구성하기 때문에 SQL Injection 을 예방할 수 있다
  - SQL 문을 컴파일한 상태기 때문에 대입된 값은 SQL 로 인식하지 않음

**단점**<br>
- 바인드 변수 부분이 "?" 로 나오므로 실행된 쿼리를 확인하기 어렵고, 따라서 쿼리에 오류가 생긴 경우 분석이 어렵다
- 미리 허용된 위치에서만 바인드 변수를 사용할 수 있기 때문에 동적 쿼리 작성이 힘들다

<br>

- - -

## 💡 Statement와 PreparedStatement 의 차이점

**1. 캐시 사용 여부**
  - Statement 는 매번 쿼리를 수행할 때마다 계속 3 단계를 수행
  - PreparedStatement 는 처음 한 번만 위 3 단계를 거친 후, 캐시에 담아 재사용

**2. SQL Injection**
- Statement 는 매번 SQL 문을 컴파일하여 실행하고 파라미터 값이 문자열로 취급되기 때문에 SQL Injection 공격에 취약
- PreparedStatement 는 미리 컴파일된 실행 계획을 사용하고, 파라미터 값이 컴파일 시에 처리되므로 SQL Injection 공격에 안전

    <details>
    <summary>Stored Procedure</summary>
    <br>

    `Stored Procedure` 는 미리 정의된 프로시저를 실행하는 방법이다. SQL 서버에 저장된 프로시저를 호출해 데이터베이스 서버에서 프로시저를 컴파일하고 실행하기 때문에 SQL Injection 공격을 방지할 수 있다.
    </details>

<br>

> 매번 다른 SQL 문을 실행하는 경우 `Statement` 를 사용하는 것이 좋다.

> 같은 SQL 문을 반복해서 실행하는 경우, SQL Injection 공격을 방지해야 하는 경우 `PreparedStatement` 를 사용하는 것이 좋다.

<br>

- - -
> 👉 참고<br>
> [[Comporison] PreparedStatement 와 Statement](https://devbox.tistory.com/133) <br>
> [Statement와 Prepared Statement의 특징](https://iksflow.tistory.com/127) <br>
> [Statement와 PreparedStatement](https://insight-bgh.tistory.com/494)
