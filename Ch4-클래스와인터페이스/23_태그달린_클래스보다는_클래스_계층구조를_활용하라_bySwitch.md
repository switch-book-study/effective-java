## 태그 달린 클래스보다는 클래스 계층구조를 활용하라
  ```
  태그 달린 클래스는 두 가지 이상의 의미를 표현할 수 있으며
  그중 현재 표현하는 의미를 태그값으로 알려주는 클래스이다.
  태그달린 클래스는 클래스 계층구조보다 훨씬 나쁘다.
  ```
  태그 달린 클래스의 단점들
  - 열거 타입선언, 태그 필드, Switch문 등 쓸데없는 코드가 많다.
  - 여러 구현이 한 클래스에 혼합돼 있어서 가독성이 나쁘다.
  - 메모리도 많이 사용한다.
  - 필드들을 final로 선언하려면 해당 의미에 쓰이지 않는 필드들까지 생성자에서 초기화해야한다. (불필요한 코드가 늘어난다)
  - `태그달린 클래스`는 `장황하고`, `오류를 내기쉽고`, `비효율적`이다.


## 클래스 계층구조를 활용하는 서브타이핑을 이용하자
  ```java
  // 태그달린 클래스를 클래스 계층구조로 변환한 예시
  //간결하고 명확하며 쓸데없는 코드도 사라진다.
  
  abstract class Figure {
    abstract double area();
  }
  
  class Circle extends Figure {
    final double radius;
    
    Circle(double radius) {this.radius = radius;}
    
    @Override double area() {return Math.PI * (radius * radius);}
  }
  
  class Rectangle extends Figure {
    final double length;
    final double width;
    
    Rectangle(double length, double width) {
      this.length = length;
      this.width = width;
    }
    
    @Override double area() {return length * width;}
  }
  ```
  
  - 정리
  ```
  태그  달린 클래스를 써야하는 상황은 거의 없다.
  새로운 클래스를 작성하는 데 태그 필드가 등장한다면
  태그를 없애고 계층구조로 대체하는 방법을 생각해보자.
  기존 클래스가 태그필드를 사용하고 있다면
  계층구조로 리팩터링 하는걸 고민해보자.
  ```
