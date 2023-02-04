## 옵셔널 반환은 신중히 하라
  - 예외는 진짜 예외적인 상황에서만 사용해야 하며
  예외를 생성할때 스택추적 전체를 캡처하므로 비용도 만만치않다.
  
  - null을 반환하면 이런 문제가 생기지는 않지만, 그 나름의 문제가 있다.
  null을 반환할 수 있는 메서드를 호출할 때는 별도의 null 처리코드를 추가해야한다.
  그러지 않으면 언젠가 NPE이 발생할 수 있다.
  
## Optional
  - 자바8부터 추가됨
  Optional<T>는 null이 아닌 T타입 참조를 하나 담거나 혹은 아무것도 담지 않을 수 있다.
  - 보다 유연하고 사용하기 쉬우며 오류가능성이 적다.
  ```java
  //컬렉션에서 최댓값을 구해 Optioanl<E>로 반환한다.
  public static <E extends Comparable<E>> Optional<E> max(Collection<E> c) {
    if (c.isEmpty())
      return Optional.empty();
  
    E result = null;
    for (E e: c)
      if (result == null || e.compareTo(result) > 0
        return = Objects.requireNonNull(e);
  
    return Optional.of(result);
  ```
  - Optional.of의 value에 null을 넣으면 NPE을 던지니 주의하자.
  - null값도 허용하는 옵셔널을 만들려면 Optional.ofNullable(value)를 사용하면 된다.
  - 옵셔널을 반환하는 메서드에서는 절대 null을 반환하지 말자.
  
## Stream에서 optional
  - stream의 종단연산 중 상당수가 optional을 반환한다.
