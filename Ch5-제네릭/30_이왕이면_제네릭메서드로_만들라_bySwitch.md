## 이왕이면 제네릭 메서드로 만들라
  - 메서드를 타입안전하게 만들어서 경고를 제거해주자.
  - 타입 매개변수들을 선언하는 타입 매개변수 목록은 메서드의 제한자와 반환타입 사이에 온다.
  ```java
  //제네릭 메서드
  public static <E> Set<E> union(Set<E> s1, Set<E> s2) {
    Set<E> result = new HashSet<>(s1);
    result.addAll(s2);
    return result;
  }
  ```
  ```java
  //제네릭 싱글턴 팩터리 패턴
  private static UnaryOperator<Object> IDENTITY_FN = (t) -> t;
  
  @SuppressWarnings("unchecked")
  public static <T> UnaryOperator<T> identityFunction() {
    return (UnaryOperator<T>) IDENTITY_FN;
  }
  ```
  ```java
  // 재귀적 타입 한정을 이용해 상호 비교할 수 있음을 표현
  public static <E extends Comparable<E>> E max(Collection<E> c);
  ```
  - 타입 한정인 `<E extends Comparable<E>>`는 `모든 타입 E는 자신과 비교할 수 있다` 라고 읽을 수 있다.
  - 즉 상호 비교 가능하다는 뜻이다.

## 정리
  ```
  클라이언트에서 입력 매개변수와 반환값을 명시적으로 형변환해야 하는 메서드보다
  제네릭메서드가 더 안전하며 사용하기 쉽다.
  타입과 마찬가지로, 메서드도 형변환 없이 사용할 수 있는 편이 좋으며,
  많은경우 그렇게 하려면 제네릭메서드가 되어야 한다.
  타입과 마찬가지로, 형변환을 해줘야 하는 기존 메서드는 제네릭하게 만들자.
  ```
