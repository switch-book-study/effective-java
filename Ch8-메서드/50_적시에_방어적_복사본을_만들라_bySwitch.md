## 적시에 방어적 복사본을 만들라.
  - 자바는 C,C++에서 흔히 보이는 버퍼오버런, 배열오버런, 와일드포인터 같은 메모리충돌 오류에서 안전하다.
  - 자바로 작성한 클래스는 시스템의 다른 부분에서 무슨짓을 하든 그 불변식이 지켜진다.

## 클라이언트가 불변식을 깨뜨리려 혈안이 되어있다고 가정하고 방어적으로 프로그래밍해야한다.
  - 아무리 자바라 해도 다른 클래스로부터의 침범을 아무런 노력 없이 다 막을 수 있는건 아니다.
  
  - 매개변수의 방어적 복사본을 만드는 예제코드
  ```java
  public Period(Date start, Date end) {
    this.start = new Date(start.getTime());
    this.end = new Date(end.getTime());
    
    if(this.start.compareTo(this.end) > 0)
      throw new IllegalArgumentException(
        this.start + "가" + this.end + "보다 늦다.");
  }
  ```
  
  - 필드의 방어적 복사본을 반환하는 예제코드
  ```java
  public Date start() {
    return new Date(start.getTime());
  }
  public Date end() {
    return new Date(end.getTime());
  }
  ```
  ```
  클래스가 클라이언트로부터 받는 혹은 클라이언트로 반환하는 구성요소가 가변이라면
  그요소는 반드시 방어적으로 복사해야한다.
  복사비용이 너무 크거나 클라이언트가 그 요소를 잘못 수정할 일이 없음을 신뢰한다면
  방어적 복사를 수행하는 대신
  해당 구성요소를 수정했을 때의 책임이 클라이언트에 있음을 문서에 명시하도록하자.
  ```
