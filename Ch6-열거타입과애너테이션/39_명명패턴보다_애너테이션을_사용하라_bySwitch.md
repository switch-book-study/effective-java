## 명명패턴보다 애너테이션을 사용하라.
## 명명패턴의 단점
  - 오타가 나면 안된다.
  - 올바른 프로그램 요소에서만 사용되리라 보증 할 방법이 없다.
  - 프로그램 요소를 매개변수로 전달할 마땅한 방법이 없다.


## 마커(marker)애너테이션 타입 선언
  ```java
  import java.lang.annotation.*;
  
  /**
  * 테스트 메서드임을 선언하는 애너테이션이다.
  * 매개변수 없는 정적 메서드 전용이다.
  */
  @Retention(RetentionPolicy.RUNTIME)
  @Target(ElementType.METHOD)
  public @interface Test {
  }
  ```
  - 이처럼 애너테이션 선언에 다는 애너테이션을 메타애너테이션이라 한다.
  ```java
  
