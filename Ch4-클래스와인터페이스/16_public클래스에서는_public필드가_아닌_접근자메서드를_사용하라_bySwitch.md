인스턴스 필드들을 모아놓는 일 외에는 아무 목적도 없는 클래스를 작성하려 할 때가 있다.
```java
//예시코드
class Point {
  public double x;
  public double y;
}
```

- 이런 클래스는 데이터 필드에 직접 접근할 수 있으니 캡슐화의 이점을 제공하지 못한다.

```java
//필드를 private으로 바꾸고 접근자를 추가한 코드

class Point {
  private double x; //public -> private
  private double y; //public -> private
  
  public Point(double x, double y) {
    this.x = x;
    this.y = y;
  }
  
  public double getX() {return x;}
  public double getY() {return y;}
  
  public void setX(double x) {this.x = x;}
  public void setY(double y) {this.y = y;}
}
```
```
public 클래스의 필드가 불변이라면 직접 노출할 때의 단점이 조금은 줄어들지만
API를 변경하지 않고는 표현방식을 바꿀 수 없고
필드를 읽을때 부수 작업을 수행할 수 없다는 단점은 여전하다.
```

정리
```
public 클래스는 절대 가변필드를 직접 노출해서는 안된다.
불변필드라도 완전히 안심할 수는 없다.

package-private 클래스나 private 중첩클래스에서는 종종 필드를 노출하는 편이 나을 때도 있다.
```
