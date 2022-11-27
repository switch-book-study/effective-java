## 톱레벨 클래스는 한 파일에 하나만 담으라
  - 소스파일 하나에 톱레벨 클래스를 여러 개 선언하는것은 아무런 득이 없고 심각한 위험을 감수해야하는 행위다.
  -어느것을 사용할지는 어느 소스파일을 먼저 컴파일하냐에 따라 달라진다.

## 톱레벨 클래스들을 서로 다른 소스파일로 분리하거나 정적멤버 클래스를 사용하자

  - 톱레벨 클래스들을 정적 멤버 클래스로 바꾼 예시
  ```java
  public class Test {
    public static void main(String[] args) {
      System.out.println(Utensil.NAME + Dessert.NAME);
    }
    
    private static class Utensil {
      static final String NAME = "pan";
    }
    
    private static class Dessert {
      static final String NAME = "cake";
    }
  }
  ```
  
## 정리
  ```
  소스파일 하나에는 반드시 톱레벨 클래스(or 인터페이스)를 하나만 담자
  이 규칙만 따른다면 컴파일러가 한 클래스에 대한 정으를 여러개 만들어 내는 일은 사라진다.
  소스파일을 어떤 순서로 컴파일하든 바이너리 파일이나 프로그램의 동작이 달라지는 일은 일어나선 안된다.
  ```
