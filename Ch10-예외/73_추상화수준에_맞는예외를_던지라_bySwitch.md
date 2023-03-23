## 추상화 수준에 맞는 예외를 던지라.
   - 상위 계층에서는 저수준 예외를 잡아 자신의 추상화 수준에 맞는 예외로 바꿔 던져야한다. (exception translation)
   ```
   메서드가 저수준 예외를 처리하지 않고 바깥으로 전파해버릴때는 내부구현 방식을 드러내어 윗 레벨 API를 오염시킨다.
   ```
   ```java
   try {
   ...
   } catch (LowerLevelException e) {
    throw new HigherLevelException(...);
   }
   ```
   
   - 예외를 번역할때 저수준예외가 디버깅에 도움이 된다면 예외연쇄를 사용하는게 좋다.
   - 예외연쇄란 문제의 근본원인인 저수준 예외를 고수준 예외에 실어 보내는 방식이다.
   ```java
   //예외연쇄
   try{
    ...
   } catch (LowerLevelExcepion cause) {
    throw new HigherLevelException(cause);
   }
   ```
   고수준 예외의 생성자는 (예외 연쇄용으로 설계된) 상위 클래스의 생성자에 이 '원인'을 건네주어 최종적으로 Throwable생성자까지 건네지게 한다.
   ```java
   예외연쇄용 생성자
   class HigherLevelException extends Exception {
    HigherLevelException(Throwable cause) {
      super(cause);
    }
  }
  ```
  - 대부분의 표준예외는 예외 연쇄용 생성자를 갖추고 있다.
  - 그렇지 않은 예외라도 Throwable의 initCause 메서드를 이용해서 원인을 직접 박을 수 있다.
  - 무턱대고 예외를 전파하는것보다는 예외번역이 낫지만 그렇다고 남용해서는 곤란하다. 예외가 발생하지 않도록 하는것이 최선이다.
  - 아래계층에서의 예외를 피할 수 없다면 상위계층에서 그 예외를 로깅등으로 조용히 처리하는 방법도 있다.
  ```
  아래 계층의 예외를 예방하거나 스스로 처리할 수 없고, 그 예외를 상위계층에 그대로 노출하기 곤란하다면 예외번역을 사용하라
  이때 예외연쇄를 이용하면 상위계층에는 맥락에 어울리는 고수준예외를 던지면서 근본 원인도 함께 알려주어 오류를 분석하기에 좋다.
  ```
