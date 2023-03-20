## 표준예외를 사용하라
  - Exception, RuntimeException, Throwable, Error는 직접 재사용하지 말자.
  ~~~
  - IllegalArgumentException 허용하지 않는값이 인수로 건내졌을때
  - IllegalStateException 객체가 메서드를 수행하기에 적절하지 않은 상태일때
  - NullPointerException Null을 허용하지 않는 메서드에 Null을 건넸을때
  - IndexOutOfBoundsException 인텍스가 범위를 넘어섰을때
  - ConcurrentModificationException 허용하지 않는 동시 수정이 발견됐을때
  - UnsupportedOperationException 호출한 메서드를 지원하지 않을때
  ~~~
  - 인수값이 무엇이었든 어차피 실패했을거라면 IllegalStateException을, 그렇지 않으면 IllegalArgumentException을 던지
