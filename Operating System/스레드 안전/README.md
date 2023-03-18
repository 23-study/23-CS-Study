# 스레드 안전(Thread-Safety)

- 정의)
    - 멀티스레드 환경에서 여러 스레드가 동시에 하나의 자원(함수, 변수, 객체)에 접근해도 프로그램의 실행에 문제가 없는 것(의도한 대로 동작하는 것)
    - 멀티스레드 환경에서 여러 스레드가 동시에 데이터를 읽거나 쓰는 등의 작업을 할 때, 데이터의 일관성과 정확성을 보장하는 것
    - 하나의 함수가 한 스레드로부터 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하여 동시에 함께 실행되더라도 각 스레드에서의 함수의 수행 결과가 올바르게 나오는 것
- 구현)
    - 스레드 안전을 보장하기 위해선 스레드 간의 동기화가 필요함
    - 더 정확히는, 공유 자원에 접근하는 임계영역(critical section)을 동기화 기법으로 제어해줘야 함 → 이를 ‘상호배제’라고 함
        - 임계구역 : 공유메모리에 접근하는 프로그램의 코드 부분
- 상호배제 구현 방법)
    - lock-based
        - 정의)
            - lock을 이용해 동기화 구현
            - 공유 자원에 하나의 Thread만 접근할 수 있도록 세마포어 / 뮤텍스로 락을 통제하는 방법
        - 예시)
            - Mutex(뮤텍스)
            - Semaphore(세마포어)
    - lock-free
        - 정의)
            - lock을 사용하지 않고 동기화 구현
            - 공유 자원에 접근할 때는 원자 연산을 이용하거나 원자적으로 정의된 접근 방법을 사용함으로써 상호 배제를 구현
        - 예시)
            - Atomic operation(원자 연산)

[Reference]

- https://developer-ellen.tistory.com/205

- https://gompangs.tistory.com/entry/OS-Thread-Safe%EB%9E%80

- https://github.com/WeareSoft/tech-interview/blob/master/contents/os.md#thread-safe
