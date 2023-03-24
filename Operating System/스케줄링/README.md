# 1. 스케줄링 알고리즘
### 1) 정의
- CPU가 Multiprogramming으로 동작할 때, 여러 프로세스나 스레드가 Ready 상태인 경우 어떤 것을 실행할지 선택하는 `스케줄러`의 알고리즘
- 이때, 스케줄러는 운영체제의 일부분임
### 2) 등장 배경
- 과거 배치 시스템 시절
  - CPU가 희귀해서 스케줄링 알고리즘 개발 활발했음
- 개인용 컴퓨터의 등장
  - 하나의 활성화된 프로세스만 존재하고 CPU는 발라져 스케줄링 알고리즘 개발 필요성 잠깐 줄어들었음
- 최근 고성능 workstation과 서버 컴퓨터 등장
  - 다수의 프로세스가 CPU 놓고 경쟁해서 스케줄링 다시 중요해짐
### 3) 발생 시점
- 프로세스 `생성`할 때 -> 생성한 프로세스와 기존 프로세스 중 선택해야 함
  - 부모 프로세스가 fork 시스템 콜을 하면 클론이 생겨서 자식 프로세스가 생성됨
  - 스케줄링은 부모 프로세스를 계속 실행할지, 자식 프로세스를 실행할지 선택해야 함 (이때, 자식과 부모는 둘 다 Ready 상태임)
- 프로세스 `종료`할 때 -> 종료한 프로세스를 대체할 프로세스를 선택해야 함
  - 프로세스가 더 이상 존재하지 않아 수행할 수 없기에, Ready 상태의 다른 프로세스가 선택되어 Running 상태로 가야 함
- 프로세스 `Block` 될 때 -> Block된 프로세스르 대체할 프로세스를 선택해야 함
  - 프로세스가 I/O, 세마포어 등과 같은 무언가 때문에 Block 상태로 가면, Ready 상태의 다른 프로세스가 선택되어 Running 상태로 가야 함
- `I/O 인터럽트`가 발생했을 때
  - I/O가 완료되면 `I/O 인터럽드`가 발생함
  - I/O가 완료되길 기다리며 Block되어 있던 프로세스가 이제 실행할 준비가 되어 Ready 상태로 옴
  - 이때 I/O 인터럽트 발생 당시 실행하던 프로세스를 계속 실행할지, 새로 Ready로 온 프로세스를 실행할지 선택해야 함
    - 일반적으론 I/O 인터럽트 때문에 억울하게 중지된 기존 프로세스를 선택함

# 2. Process Switching (Context Switching)
- 정의) Running 상태의 프로세스를 끌어내리고 Ready 상태의 프로세스를 Running으로 올려주는 것
- 특징) Expensive해서 `스케줄링` 잘해줘야 함
- 과정) 
    - user 모드에서 Kernel 모드로 전환
    - 프로세스 테이블에 현재 끌어내릴 프로세스의 상태를 store 함
    - `스케줄링 알고리즘` 실행해 새 프로세스 선택
    - 새 프로세스의 저장 상태 load 해와서 실행시킴


# 3. 스케줄링 알고리즘의 분류
### 1) Clock Interrupt 처리 유무에 따라 분류
- Clock Interrupt
  - 하드웨어 Clock이 주기적으로 Clock Interrupt를 발생시킴
  - 매 Clock Interrupt 혹은 K번째 Clock Interrupt마다 스케줄링 결정 이루어짐
- Nonpreemptive(비선점) 스케줄링 알고리즘 : `Clock Interrupt 처리 X`
  - 실행 프로세스는 Block되거나 자발적으로 CPU 내놓을 때까지 계속 실행될 수 있음
  - 수 시간동안 계속 수행해도 강제 중단 안됨
- Preemptive(선점형) 스케줄링 알고리즘 : `Clock Interrupt 처리 O`
  - 실행 프로세스는 할당된 시간을 넘지 않는 범위에서 실행됨
  - 할당된 시간 다 되면 중단되어 Ready 상태로 끌어내려짐
### 2) 시스템 환경에 따라 분류
- 배치(Batch) 시스템
- 대화식(Interactive) 시스템
- 실시간(Real time) 시스템

# 4. 배치(Batch) 시스템의 스케줄링 알고리즘
### 1) 선입선출 (First-Come First-Served)
### 2) 최단작업우선(Shortest Job First)
### 3) 최단잔여시간우선(Shortest Remaining Time Next)

# 5. 대화식(Interactive) 시스템의 스케줄링 알고리즘
### 1) 라운드 로빈 스케줄링(Round-Robin Scheduling)
### 2) 우선순위 스케줄링(Priority Scheduling)
### 3) 최단프로세스순번(Shortest Process Next)
### 4) 보장 스케줄링(Guaranted Scheduling) 
### 5) 복권 스케줄링(Lottery Scheduling)
### 6) 공평-몫 스케줄링(Fair-Share Scheduling)

# 6. 실시간(Real time) 시스템에서 스케줄링

# 7. 스레드 스케줄링(Thread Scheduling)

- 출처
  - 작년 운체 수업 듣고 정리해 둔 것 보고 하나하나 직접 다시 쓰면서 좀 더 보기 편하게 정리해봤어요
