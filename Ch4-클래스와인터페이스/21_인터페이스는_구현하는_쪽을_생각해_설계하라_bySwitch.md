- 
```
디폴트 메서드를 선언하면, 그 인터페이스를 구현한 후 
디폴트 메서드를 재정의하지 않은 
모든 클래스에서 디폴트 구현이 쓰이게 된다.
```
```
- 자바에도 기존 인터페이스에 메서드를 추가하는 길이 자바8 이후 등장했지만
- 모든 기존 구현체들과 매끄럽게 연동되리라는 보장은 없다.
```
- 디폴트 메서드는 구현 클래스에 대해 아무것도 모른 채 합의없이 무작정 `삽입`될 뿐이다.
 
- 생각할 수 있는 모든 상황에서 불변식을 해치지 않는 디폴트 메서드를 작성하기란 어려운 법이다.
```java
//자바8의 Collection 인터페이스에 추가된 디폴트 메서드
default boolean removeIf(Predicate<? super E> filter) {
  Objects.requireNonNull(filter);
  boolean result = false;
  for (Iterator<E> it = iterator(); it.hasNext(); ) {
    if (filter.test(it.next())) {
      it.remove();
      result = true;
    }
  }
  return result;
}
```
- 디폴트 메서드는 컴파일에 성공하더라도 기존 구현체에 런타임 오류를 일으킬 수 있다.
- 인터페이스를 설계할 때는 세심한 주의를 기울여야 한다.
