## 로 타입은 사용하지 말라
  - 로 타입이란? 제네릭 타입에서 타입 매개변수를 전혀 사용하지 않을 때를 말한다. ex) List<E>의 로 타입은 List다.
  
## 제네릭을 활용해서 타입 안전성을 확보
  ```java
  //매개변수화된 컬렉션 타입
  private final Collection<Stamp> stamps = ...;
  ```
  - 
