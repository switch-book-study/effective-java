## 스트림 병렬화는 주의해서 적용하라
  ```
  계산도 올바로 수행하고 성능도 빨라질 거라 확신 없이는 스트림 파이프라인 병렬화는 시도조차 하지 말라.
  스트림을 잘못 병렬화하면 프로그램을 오작동하게 하거나 성능을 급격히 떨어뜨린다.
  병렬화하는 편이 낫다고 믿더라도, 수정 후의 코드가 여전히 명확한지 확인하고
  운영환경과 유사한 조건에서 수행해보며 성능지표를 유심히 관찰하라.
  그래서 계산도 정확하고 성능도 좋아졌음이 확실해졌을때, 오직 그럴때만 병렬화 버전 코드를 운영코드에 반영하라.
  ```
  
## 동시성 프로그래밍을 할때는 안전성과 응답 가능상태를 유지하기위해 힘써야한다.
  - 데이터 소스가 Stream.iterate거나 중간 연산으로 limit를 쓰면 파이프라인 병렬화로는 성능 개선을 기대할 수 없다.
  ```
  대체로 스트림의 소스가 ArrayList, HashMap, HashSet, ConcurrentHashMap의 인스턴스거나
  배열, int범위 long범위 일 때 병렬화의 효과가 가장 좋다.
  ```
  ```
  ArrayList, HashMap, HashSet, ConcurrentHashMap 자료 구조들은
  데이터를 원하는 크기로 정확하고 손쉽게 나눌 수 있어서
  다수의 스레드에 일을 분배하기 좋은 특징이 있다.
  
  또한 원소들을 순차적으로 실행할 때의 참조 지역성(locality of reference)이 뛰어나다는 것이다.
  이웃한 원소의 참조들이 메모리에 연속해서 저장되어 있다는 뜻이다.
  ```
  
  ```
  참조 지역성이 가장 뛰어난 자료구조는 기본 타입의 배열이다.
  기본타입배열에서는 참조가 아닌 데이터 자체가 메모리에 연속해서 저장되기 때문이다.
  ```
  
## 스트림 파이프라인의 종단연산 동작방식 역시 병렬 수행효율에 영향을 준다.
  - 종단 연산 중 병렬화에 가장 적합한것은 축소(reduction)이다.
    - ex) reduce 메서드 중 하나, min, max, count, sum 같이 완성된 형태로 제공되는 메서드
    - anyMatch, allMatchm noneMatch처럼 조건에 맞으면 바로 반환되는 메서드도 병렬화에 적합하다.
    
  - 가변축소(mutable reduction)를 수행하는 Stream의 collect 메서드는 병렬화에 적합하지 않다.
    - 컬렉션들을 합치는 부담이 크다.
    - Stream, Iterable, Collection이 병렬화 이점을 누리게하려면 spliterator 메서드를 재정의하고 성능을 테스트해야한다.
   
## 스트림을 잘못 병렬화하면 성능이 나빠질 뿐 아니라 결과자체가 잘못되거나 예상못한 동작이 발생할 수 있다.


## 조간이 잘 갖춰지면 parallel 메서드 호출 하나로 거의 프로세서 코어 수에 비례하는 성능향상을 만끽할 수도 있다.

