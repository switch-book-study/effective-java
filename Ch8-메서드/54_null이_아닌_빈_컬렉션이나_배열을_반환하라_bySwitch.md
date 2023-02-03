## null이 아닌 빈 컬렉션이나 배열을 반환하라
  
  ```java
  //빈 컬렉션을 반환하는 올바른 예
  public List<Cheese> getCheeses() {
    return new ArrayList<>(cheesesInStock);
  }
  ```
  - 빈 컬렉션과 배열은 굳이 새로 할당하지 않고도 반환할 수 있다.
  ```
  ```java
  //최적화- 빈 컬렉션을 매번 새로 할당되지 않도록 했다.
  public List<Cheese> getCheeses() {
    return cheesesInStock.isEmpty() ? Collections.emptyList()
      : new ArrayList<>(cheesesInStock);
  }
  ```
  - 배열도 마찬가지다.
  ```java
  //길이가 0일수도 있는 배열을 반환하는 올바른 방법
  public Cheese[] getCheeses() {
    return cheesesInStock.toArray(new Cheese[0]);
  }
  
  //최적화 - 빈 배열을 매번 새로 할당하지 않도록 했다.
  private static final Cheese[] EMPTY_CHEESE_ARRAY = new Cheese[0];
  public Cheese[] getCheeses(){
    return cheesesInStock.toArray(EMPTY_CHEESE_ARRAY);
  }
  ```
  
  ```
  null이 아닌 빈 배열이나 컬렉션을 반환하라.
  null을 반환하는 API는 사용하기 어렵고 오류처리코드도 늘어난다.
  그렇다고 성능이 좋은것도 아니다.
  ```
