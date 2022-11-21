## 자바의 다중 구현 메커니즘
  1. 추상 클래스
  2. 인터페이스
  - 자바는 단일 상속만 지원한다.

##
  - 인터페이스는 `믹스인` 정의에 안성맞춤이다.
  - Coimparable
   - 자신을 구현한 클래스의 인스턴스들 끼리는 순서를 정할 수 있다고 선언하는 믹스인 인터페이스

## 인터페이스로 계층구조가 없는 타입 프레임워크를 만들 수 있다.
  ```java
  public interface Singer {
    AudioClip sing(Song s);
  }
  public interface Songwriter {
    Song compose(int chartPosition);
  }
  
  public interface SingerSongwriter extends Singer, Songwriter {
    AudioClip strum();
    void actSensitive();
  }
  ```
  - 예제정도의 `유연성`이 항상 필요하지는 않지만, 이렇게 만들어둔 인터페이스가 결정적인 도움을 줄 수도 있다.
  - 같은구조를 클래스로 만드려면 가능한 조합 전부를 각각 정의한 `고도비만 계층구도`가 만들어질것이다.
  - 흔히 `조합폭발`이라 부르는 현상이다.
  - 래퍼클래스 관용구와 함께 사용하면 `인터페이스는 기능을 향상시키는 안전하고 강력한 수단`이 된다.


