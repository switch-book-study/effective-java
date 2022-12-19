## 비트필드 대신 EnumSet을 사용하라
  ```java
  //EnumSet - 비트필드를 대체하는 현대적 기법
  public class Text {
    public enum Style { BOLD, ITALIC, UNDERLINE, STRIKETHROUGH }
    
    //어떤 Set을 넘겨도 되나, EnumSet이 가장 좋다.
    public void applyStyles(Set<Style> style) {...}
  }
  ```
  - 정리
  ```
  열거할 수 있는 타입을 한데 모아 집합형태로 사용한다고 해도 비트필드를 사용할 이유는 없다.
  EnumSet클래스가 비트필드수준의 명료함과 성능을 제공하고 열거타입의 장점까지 선사한다.
  ```
 
