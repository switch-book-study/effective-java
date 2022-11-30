## 비검사 경고를 제거하라
- 할 수 있는 한 모든 비검사 경고를 제거하라
```
곧바로 해결되지 않는 경고가 나타나도 포기하지 말자
모두 제거한다면 그 코드는 타입 안정성이 보장된다.
```
- 경고를 제거할 수는 없지만 타입 안전하다고 확신할 수 있다면 @SuppressWarnings("unchecked") 애너테이션을 달아 경고를 숨기자.
- @SuppressWarnings 애너테이션은 항상 가능한 한 좁은 범위에 적용하자

```java
//지역변수를 추가해 @SuppressWarnings의 범위를 좁힌다.
public <T> T[] toArray(T[] a) {
  if (a.length < size) {
    //생성한 배열과 매개변수로 받은 배열의 타입이 모두 T[]로 같으므로 올바른 형변환이다.
    @SuppressWarnings("unchecked") T[] result =
      (T[]) Arrays.copyOf(elements, size, a.getClass());
    return result;
  }
  System.arraycopy(elements, 0, a, 0, size);
  if (a.length > size) {
    a[size] = null;
  }
  return a;
}
```
- @SuppressWarnings("unchecked") 애너테이션을 사용할 때면 그 ㄱㅇ고를 무시해도 안전한 이유를 항상 주석으로 남겨야한다.

## 정리
```
비검사 경고는 중요하니 무시하지 말자
모든 비검사경고는 런타임에 ClassCastException을 일으킬 수 있는 잠재적 가능성을 뜻하니 최선을 다해 제거하라.
경고를 없앨 방법을 찾지 못하겠다면, 
그 코드가 타입 안전함을 증명하고 
가능한 한 범위를 좁혀 @SuppressWarnings("unchecked")애너테이션으로 경고를 숨겨라.
그런다음 경고를 숨기기로 한 근거를 주석으로 남겨라.
```
