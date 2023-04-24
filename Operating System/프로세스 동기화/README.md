## 프로세스 동기화

- 정의) 여러 개의 프로세스나 스레드가 공유 자원을 사용할 때, 경쟁 상태를 막기 위한(데이터의 무결성과 일관성을 보장하기 위한) 기법
- 관련 용어)
    - 경쟁 상태(Race Condition)
        - 정의) 둘 이상의 프로세스가 동시에 공유데이터에 접근할 때 누가 언제 수행되느냐에 따라 결과 바뀌는 상황
        - 예시) 스풀러 디렉터리
        - 방지 조건)
            1. 상호 배제 제공해 어느 두 프로세스도 동시에 임계구역에 있지 못하게 함
            2. CPU 개수나 속도에 대한 가정을 하지 않음
            3. 임계구역 밖의 프로세스는 다른 프로세스를 block시키면 안 됨 (임계구역에 들어가려는 다른 프로세스 막으면 안되서)
            4. 임계구역에 들어가려고 무한히 기다리는 프로세스 없어야 함
    - 상호 배제(Mutual Exclusion)
        - 정의) 한 프로세스가 공유데이터 읽거나 쓰고 있으면 다른 프로세스들은 똑같은 일을 수행하지 못하도록 하는 것
    - 임계 구역(Critical Region)
        - 정의) 공유메모리에 접근하는 프로그램의 코드 부분.
            - 공유메모리 그 자체 아님.
    - 바쁜 대기(Busy Waiting)
        - 정의) 변수가 특정 값이 될 때까지 계속 검사하는 것
        - 특징)
            - CPU 시간이 낭비되기에 기다리는 시간이 짧을 것으로 예상될 때만 사용함
            - 스핀 락 : 바쁜 대기를 사용하는 락

## 바쁜 대기 쓰는 상호배제

### 1) 인터럽트 끄기 → 비추천(권한 남용)

- 정의) 임계구역에 진입한 직후 모든 인터럽트를 비활성화하고, 떠나기 직전 다시 활성화함
    - 인터럽트 비활성화하면 process switch가 일어나지 않아서 상호배제가 제공됨
- 단점) 사용자 프로세스에게 인터럽트를 껐다 켤 수 있는 권한 주는 거라 바람직 x

### 2) 락 변수 사용(Lock Variables) → 실패(조건 1_상호배제 x)

- 락 변수 : 임계구역에 프로세스가 있고 없고를 나타내는 공유변수.
    - 0이면 임계구역에 프로세스 없음.
    - 1이면 임계구역에 프로세스 있음.
- 정의) 임계구역 들어가기 전에 락 변수를 살펴봄.
    - 0 → 1로 변경하고 임계 영역에 들어감.
    - 1 → 0이 될 때까지 기다림
- 단점) Lock 검사 후 값 변경하는 사이에 스위치 일어나면 상호배제 깨짐

### 3) 엄격한 교대(Turn) → 실패(조건 3_x)

- Turn 변수 : 임계구역에 진입할 순번 나타내는 공유변수.
    - 0이면 A차례
    - 1이면 B차례
- 정의) 임계구역 들어가기 전에 turn 변수를 살펴봄.
    - A
        
        ```c
        while(true) {
        	while (turn!=0); // 조건 거짓(turn=0)이면 바로 빠져나감
        	critical_region();
        	turn = 1;
        	noncritical_region();
        }
        ```
        
        - 0 → 1로 변경하고 임계 영역에 들어감.
        - 1 → 0이 될 때까지 기다림
    - B
        
        ```c
        while(true) {
        	while (turn!=1); // 조건 거짓(turn=1)이면 바로 빠져나감
        	critical_region();
        	turn = 0;
        	noncritical_region();
        }
        ```
        
        - 1 → 0로 변경하고 임계 영역에 들어감.
        - 0 → 1이 될 때까지 기다림
- 장점) 조건1_상호배제 제공함
- 단점) 조건3 위반
    - 비임계구역의 프로세스가 다른 프로세스를 차단함
    - 예시)
        - B가 임계구역 실행 후 turn=0으로 변경함
        - A는 임계구역 실행 후 turn=1로 변경함
        - B는 비임계구역 실행 중임
        - A가 B보다 먼저 임계구역 실행을 원한다면?
            - A는 B가 다시 임계구역 실행해서 turn을 0으로 변경해줄 때까지 block됨

### 4) Peterson의 해법 → 성공(Turn 변형)

- interested[N] : 임계구역에 들어가고 싶은 의사를 표현 (관심 있음을 표현)
    - interested[0]의 값이 true면 프로세스 0이 임계구역에 들어가고 싶은 의사를 표현한 것
- 정의) 임계구역 들어가기 전에 turn 변수와 interested 변수를 살펴봄
    
    ```c
    #define FALSE 0
    #define TRUE 1 
    #define N 2 // 프로세스 개수
    int turn; // 누구 차례인가. 0이나 1
    int interested[N]; // 모든 값은 0(FALSE)으로 초기화. 누가 관심있는가
    
    void enter_region(int process) { // 프로세스 0 혹은 1
    	int other; // 상대방 프로세스의 번호
    	other = 1-process;
    	interested[process] = TRUE; // 나 관심있어
    	turn = process; // 현재 차례는 나야!
    	while (turn == process && interested[other] == TRUE)
    }
    
    void leave_region(int process) { // 프로세스 0 혹은 1
    	interested[process] = FALSE; // 나 이제 관심 없어
    }
    ```
    
- 장점) 엄격한 교대 요구하지 않으면서 상호 배제 제공함

### 5) TSL 명령 (Lock + 하드웨어)

- 정의) Lock 변수 값을 register에 복사해두고 lock 변수값을 무조건 1로 세팅한 후, register에 복사해둔 이전 Lock값을 살펴봄
    - 0 → 1로 변경하고 임계 영역으로 들어감
    - 1 → 0이 될 때까지 대기함
    
    ```nasm
    enter region:
    	TSL REGISTER, LOCK // lock 값 읽어서 레지스터에 저장하고, lock값을 1로 설정함
    	CMP REGISTER, #0 // 아까 저장한 lock값이 0이니?
    	JNE enter_region // (not equal) lock값 1이라면, lock은 세팅되어있는 애란 소리니 loop 돔
    	// 현재 임계구역에 있는 프로세스가 임계구역 작업 마치면 0이 되겠지.
    	RET // enter region 호출한 애로 return됨.
    	// 즉, 임계구역 들어감.
    
    leave_region:
    	MOVE LOCK, #0 // lock에 0을 저장함.
    	RET // 호출자로 return됨.
    	// 락 반환은 프로세스가 0 저장하기만 하면 됨.
    ```
    
- TSL 명령
    - test and set lock
    - lock 값 읽어서 레지스터에 저장하고 lock에 0이 아닌 값을 저장함
        
        → 하나의 연산. 분할 불가능. 연산 중간에 process switch 일어날 수없음
        
    - TSL 명령 수행 끝날 때까지 메모리 버스 잠겨서 다른 어떤 CPU도 메모리 접근 불가함
    - vs. 인터럽트 비활성화 → 인터럽트 끄는 것은 다른 CPU 못막음
- 특징)
    - 하드웨어 도움 받음
    - 분할 불가능함(indivisible)
- 단점)
    - 프로세스가 enter_region, leave_region을 제때 호출안하면 상호배제 실패함

## 바쁜 대기 안 쓰는 상호배제

### 1) 바쁜 대기의 단점

- 임계구역 진입이 허용되지 않을 때 루프를 돌며 CPU 시간 낭비

### 2) Sleep and Wakeup → 실패(Race Condition 발생)

- 정의) 임계구역 진입이 허용되지 않을 때 바쁜 대기 안하고, block함
- Sleep
    - 호출자를 block 상태로 만드는 시스템 호출
    - 다른 프로세스가 Wakeup 시스템 호출로 깨워줄 때까지 block 상태에 머물게 됨
- Wakeup
    - 깨울 프로세스를 인자로 가져 깨워서 ready 상태로 보내주는 시스템 호출
- 사용 예) 생산자-소비자 문제
    - 정의) 생산자는 공유버퍼에 아이템 계속 생산하고, 소비자는 아이템 계속 소비하는 개념
        - 두 프로세스가 고정된 크기의 버퍼를 공유함
        - 생산자가 정보를 버퍼에 넣고, 소비자는 정보를 버퍼에서 꺼내옴
    - 해결)
        - 생산자가 새로운 아이템을 버퍼에 넣고 싶은데 버퍼가 이미 꽉 찬 경우 소비자가 버퍼에서 아이템 꺼내갈 때까지 sleep 상태가 됨
        - 소비자가 아이템 버퍼에서 꺼내오고 싶은데 버퍼에 아무것도 없는 경우 생산자가 버퍼에 아이템 넣어줄 때까지 sleep 상태가 됨
        - 따라서, 생산자는 아이템 넣었을 때 소비자를 wakeup 해줘야하고, 소비자는 아이템 꺼내 제거했을 때 생산자를 wakeup 해줘야함.
    
    ```c
    #define N 100 // 버퍼 크기
    int count=0; // 버퍼에 있는 아이템 개수
    
    void producer(void) // 생성자
    {
    	int item;
    
    	while(TRUE) { // 무한 반복
    		item = produce_item(); // 다음 아이템 생성
    		if(count==N) sleep(); // 버퍼 꽉 차있으면 sleep
    		insert_item(item); // 버퍼에 아이템을 넣음
    		count+=1; // 카운트를 1 증가시킴
    		if(count==1) wakeup(consumer); // 버퍼에 아이템 없던 상테어서 한 개 된 상태라면 
    		// 소비자 깨움
    	}
    }
    
    void consumer(void) // 소비자
    {
    	int item;
    
    	while(TURE) { // 무한 반복
    		if(count==0) sleep(); // 버퍼 비어있으면 sleep
    		item = remove_item(); // 버퍼에서 아이템 꺼내옴(pop)
    		count-=1; // 카운트 1 감소시킴
    		if(count==N-1) wakeup(producer); // 버퍼에 아이템이 꽉 찬 상태에서 한 개 빠진 상태라면 
    		// 생성자 깨움
    		consume_item(item); // 아이템을 출력함
    	}
    }
    ```
    
    - 단점
        - 정의) 아직 sleep 상태가 아닌 프로세스에게 wakeup 전송하는 경우 wakeup이 소실되어 둘다 영원히 잠들게 되는 결과 초래됨
        - 원인) sleep() 콜하기 직전에 process switch 일어나면(교묘하게 스케줄링 되면) sleep() 안된 상태로 wakeup() 받는 상황 발생함

### 3) 세마포어

- 정의) 미래를 위해 미리 호출한 wakeup 회수를 저장해주는 변수 타입
    - 다익스트라가  제안한 새로운 변수 타입
    - 정수 변수
        - 0 → wakeup이 저장 안됨
        - 양수값 → 하나 이상의 wakeup이 대기 중
- 장점) 경쟁조건 방지, 동기화 문제 해결
    - 세마포어 연산의 원자성이 보장되어 연산 시작하면 연산 완료되거나 프로세스가 잠들 때까지 다른 프로세스가 세마포어에 접근 불가
- 연산
    - down(P)
        
        ```c
        if(P > 0) { // 세마포어 값이 0보다 큰지 검사
        	P--; // 0보다 크면 세마포어 감소시켜 세마포어에 저장된 wakeup하나를 소비하고 수행 계속함
        } else if(P = 0) {
        	sleep(); // 0이면 프로세스는 down연산 완료 안 한 채 바로 잠듦
        }
        ```
        
    - up(V)
        
        ```c
        V++; // 세마포어의 값을 증가시킴
        if(sleeping process exist in V) { // 하나 이상의 프로세스가 down 완료 못한채 세마포어에서 잠들어있으면 
        	wakeup(); // 그 중 한 프로세스가 시스템에 의해 선택되어 깨워져 down 완료함.
        }
        ```
        
    - mutual exclusion 제공하는 법: down 연산 → critical region → up 연산
    - up, down연산은 원자성 보장되어 실행 중 중단되지 않음.
        - 일반적으로 인터럽트 비활성화하는 시스템호출로 구현됨
        - 따라서 down에서 세마포어 값 검사한 후 감소시키는 중간에 process switch가 일어나지 않음.
- 사용 예) 생산자-소비자 문제
    
    ```c
    #define N 100 // 버퍼 크기
    typedef int semaphore; // semaphore라는 타입 정의. 특별한 int임
    semaphore mutex=1; // 생산자와 소비자가 동시에 버퍼 접근 못하게 함
    semaphore empty=N; // 빈 슬롯의 개수
    semaphore full=0; // 아이템으로 채워진 슬롯의 개수
    
    void producer(void) { // 생산자
    	int item;
    	while(TRUE) {
    		item = produce_item(); // 버퍼에 넣을 아이템 생성
    		down(&empty); // 빈 슬롯의 개수(empty) 확인함. 
    		down(&mutex); // 임계지역에 들어감.
    		insert_item(item); // 임계지역 - 새 아이템을 버퍼에 넣음 (하나 넣어)
    		up(&mutex); // 임계 지역에서 나옴
    		up(&full); // 아이템으로 채워진 슬롯의 개수 증가시킴
    	}
    }
    
    void consumer(void){ // 소비자
    	int item;
    
    	while(TRUE) {
    		down(&full); // 아이템으로 채워진 슬롯의 개수를 감소시킴
    		down(&mutex); // 임계 지역에 들어감
    		item=remove_item(); // 임계지역 - 버퍼에서 아이템 꺼내옴 (하나 뽑아)
    		up(&mutex); // 임계지역에서 나옴
    		up(&empty); // 빈 슬롯의 개수를 증가시킴
    		consume_item(item); // 아이템을 출력함
    	}
    }
    ```
    

### 4) 뮤텍스

- 정의) 세마포어의 개수 세는 능력이 빠진 단순화된 버전
    - 언락: 임게구역 사용 가능 → 0
    - 락: 임계구역 사용 안됨 → 1
- 특징)
    - 상호배제용으로 씀
        - mutex_lock, critical region, mutex_unlock 순으로 사용
    - 뮤텍스는 세마포어가 아님
    - 스레드 패키지에 유용
    - 프로시저 레벨이 아닌 스레드 레벨에서 부르는 코드

### 5) 모니터

- 정의) 모듈 또는 패키지에 모아진 프로시듀어, 변수, 자료구조의 모음
- 특징)
    - 높은 수준의 동기화 프리미티브
    - 상호배제 제공
        - 단 하나의 프로세스만 한 순간에 모니터에서 활동 가능
            - 모니터의 자료구조는 모니터 내부의 프로시듀어만 직접 접근 가능하고,
            - 프로세스는 모니터의 프로시듀어를 호출함
            - 모니터 프로시듀어 호출 시 다른 프로세스가 모니터에서 활동 중인지 검사함
                - 활동 중인 프로세스 O → 다른 프로세스가 모니터에서 나올 때까지 중단됨
                - 활동 중인 프로세스 X → 모니터에 진입함
        - 상호배제 구현은 이진 세마포어나 뮤텍스 사용해 컴파일러가 함. (잘못될 가능성↓)
- 단점
    - 컴파일러에서 지원해야 함
    - 분산 환경에서 적용할 수 없음
- 코드
    
    ```c
    monitor example
    	integer i;
    	condition c;
    	procedure producer();
    	...
    	end;
    	procedure consumer();
    	...
    	end;
    end monitor;
    ```
