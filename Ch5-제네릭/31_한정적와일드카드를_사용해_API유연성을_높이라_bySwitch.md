## 한정적 와일드카드를 사용해 API 유연성을 높이라
  - 매개변수화 타입은 불공변이다.
  ```
  List<Type1>은 List<Type2>의 하위타입도 상위타입도 아니다.
  예를들어 List<String>은 List<Object>의 하위타입이 아니라는 뜻이다.
  List<String>은 List<Object>가 하는 일을 제대로 수행하지 못하니 하위타입이 될 수 없다.
  ```
  - 한정적 와일드카드 타입으로 불공변을 보다 유연하게 할 수 있다.
  ```java
  //E 생산자(producer) 매개변수에 와일드카드 타입 적용
  public void pushAll(Iterable<? extends E? src) {
    for (E e : src)
      push(e);
  }
  ```
  ```java
  //E 소비자(consumer)매개변수에 와일드카드 타입 적용
  public void popAll(Collection<? super E> dst) {
    while (!isEmpty()
      dst.add(pop());
  }
  ```
  - 유연성을 극대화하려면 원소의 생산자나 소비자용 입력매개변수에 와일드카드 타입을 사용하라
  - 
