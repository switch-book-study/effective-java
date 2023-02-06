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
  ```java
  public static <E extends Comparable<E>> Optional<E> max(Collection<E> c) {
    return c.stream().max(Comparator.naturalOrder());
  }
  ```
  - 옵셔널은 검사예외와 취지가 비슷하다.
  
  - 옵셔널 활용
  ```java
  //기본값을 정해두기
  String lastWordInLexicon = max(words).orElse("단어없음");
  
  //원하는 예외 던지기
  Topy myToy = max(toys).orElseThrow(TemperTantrumException::new);
  
  //값이 항상 있다고 가정하기
  Element lastNobleGas = max(Elements.NOBLE_GASES).get();
  ```
  
## 사용
  - 무조건 반환값으로 옵셔널을 사용한다고 해서 득이되는건 아니다.
     컬렉션, 스트림, 배열, 옵셔널같은 컨테이너 타입은 옵셔널로 감싸면 안되고 빈 컨테이너를 반환하는게 좋다.
  - 결과가 없을 수 있으며 클라이언트가 이 상황을 특별하게 처리해야 한다면 Optional<T>를 반환하면 된다.
  ```
  정리 
  
  값을 반환하지 못할 가능성이 있고, 호출할 때마다 반환값이 없을 가능성을  염두에 둬야 하는 메서드라면
  옵셔널을 반환해야 할 상황일 수 있다.
  
  하지만 옵셔널 반환에는 성능 저하가 뒤따르니, 성능에 민감한 메서드라면 null을 반환하거나 예외를 던지는 편이 나을 수 있다.
  
  그리고 옵셔널을 반환값 이외의 용도로 쓰는 경우는 매우 드물다.
  ```
  
