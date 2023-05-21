## 데이터베이스 샤딩이란?

대규모 데이터베이스를 여러 머신에 저장하는 프로세스

데이터를 샤드라고 하는 더 작은 청크로 분할하고 여러 데이터베이스 서버에 저장함으로써 이러한 한계를 극복한다
모든 데이터베이스 서버의 기본 기술은 일반적으로 동일하며 함께 작동하여 대량의 데이터를 저장하고 처리한다
* application level에서도 가능하지만 database level에서도 가능하다
* Horizontal Partitioning이라고 볼 수 있다

[필요한 원리]
1. 분산된 Database에서 Data를 어떻게 Read할 것인가?
2. 분산된 Database에 Data를 어떻게 잘 분산시켜서 저장할 것인가?
    분산이 잘 되지 않고, 한쪽으로 Data가 몰리게 되면 자연스럽게 Hotspot이 되어 성능이 느려지게 됨
    그렇기 때문에 균일하게 분산하는 것이 중요한 목표

샤딩의 이점

응답 시간 개선

전체 서비스 중단 방지

효율적인 크기 조정


[샤딩] Sharding을 적용한다는 것은?</br>

  1.  프로그래밍, 운영적인 복잡도는 더 높아지는 단점이 있다</br>
  2.  가능하면 Sharding을 피하거나 지연시킬 수 있는 방법을 찾는 것이 우선되어야 한다</br>
  * Scale-in</br>
    Hardware Spec이 더 좋은 컴퓨터를 사용한다
    
  * Read부하가 크다면?</br>
    Cache나 Database의 Replication을 적용하는 것도 하나의 방법
    
  * Table의 일부 컬럼만 자주 사용한다면?</br>
    Vertically Partition도 하나의 방법
    Data를 Hot, Warm, Cold Data로 분리하는 것
    
    
