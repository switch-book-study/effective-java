
- 상속은 캡슐화를 해친다.
- 상속은 상위클래스와 하위클래스가 순수한 is-a 관계일때만 써야한다.
- 상속의 취약점을 피하려면 상속대신 컴포지션과 전달을 사용하자.
- 특히 래퍼클래스로 구현할 적당한 인터페이스가 있다면 더욱 그렇다.
- 래퍼클래스는 하위클래스보다 견고하고 강력하다

```java
//래퍼클래스 - 상속대신 컴포지션을 사용 한 예시
public class InstrumentedSet<E> extends ForwardingSet<E> {
  private int addCount = 0;
  
  public InstrumentedSet(Set<E> s) {
    super(s);
  }
  
  @Override
  public boolean add(E e) {
    addCount++;
    return super.add(e);
  }
  
  @Override
  public boolean addAll(Collection<? extends E> c) {
    addCount += c.size();
    return super.addAll(c);
  }
  
  public int getAddCount() {
    return addCoount;
  }
}
```
