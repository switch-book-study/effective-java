## 매개변수가 유효한지 검사하라
  ```
  메서드나 생성자를 작성할 때면 그 매개변수들에 어떤 제약이 있을지 생각해야한다.
  그 제약들을 문서화하고 메서드 코드 시작부분에서 명시적으로 검사해야 한다.
  ```
  - public과 protected 메서드는 매개변수값이 잘못 됐을때 던지는 예외를 문서화해야한다.
    (@throws 자바독 태그를 이용)
  ```java
  /**
  * (현재 값 mod m) 값을 반환한다.
  * 이 메서드는 항상 음이 아닌 BigInteger를 반환한다는 점에서 remainder 메서드와 다르다.
  * 
  * @param m 계수(양수여야 한다.)
  * @return 현재 값 mod m
  * @throws ArithmeticException m이 0보다 작거나 같으면 발생한다.
  */ 
  public BigInteger mod(BigInteger m) {
    if (m.signum() <= 0)
      throw new ArithmeticException("계수(m)는 양수여야 합니다. " + m);
    ...//계산 수행
  }
  ```
