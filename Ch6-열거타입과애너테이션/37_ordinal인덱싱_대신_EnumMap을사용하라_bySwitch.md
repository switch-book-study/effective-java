## ordinal 인덱싱 대신 EnumMap을 사용하라
  ```
  배열의 인덱스를 얻기 위해 ordinal을 쓰는것은 일반적으로 좋지 않다.
  대신 EnumMap을 사용하자.
  다차원 관계는 EnumMap<..., EnumMap<...>>으로 표현하자.
  애플리케이션 프로그래머는 Enum.ordinal을 웬만해서는 사용하지 말아야한다
  ```
