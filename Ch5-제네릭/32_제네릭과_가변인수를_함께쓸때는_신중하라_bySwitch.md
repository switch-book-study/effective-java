## 제네릭과 가변인수를 함께 쓸 때는 신중하라
  - 제네릭 varargs배열 매개변수에 값을 저장하는 것은 타입 안전하지 않다.

## @SafeVarargs
  -  @SafeVarargs 애너테이션은 메서드 작성자가 그 메서드가 타입 안전함을 보장하는 장치다.
  -  메서드가 안전한게 확실하지 않다면 절대 @SafeVarargs를 달면 안된다.
  -  
## 제네릭 varargs 매개변수를 안전하게 사용하는 메서드
  ```java
  @SafeVarargs
  static <T> List<T> flatten(List<? extends T? ... lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
      result.addAll(list);
    return result;
  ```
  - 제네릭이나 매개변수화 타입의 varargs 매개변수를 받는 모든 메서드에 @SafeVarargs를 달라.

  ```
  @SafeVarargs 애너테이션은 재정의할 수 없는 메서드에만 달아야 한다.
  재정의한 메서드도 안전할지는 보장할 수 없기 때문이다.
  ```
  
## 정리
  ```
  가변인수와 제네릭은 궁합이 좋지 않다.
  가변인수 기능은 배열을 노출하여 추상화가 완벽하지 못하고 배열과 제네릭의 타입 규칙이 서로 다르기 때문이다.
  제네릭 varags매개변수는 타입 안전하지는 않지만 허용된다.
  메서드에 제네릭 varargs매개변수를 사용하고자 한다면 먼저 그 메서드가 타입 안전한지 확인한다음
  @SafeVarargs애너테이션을 달아 사용하는데 불편함이 없도록 하자.
  ```
