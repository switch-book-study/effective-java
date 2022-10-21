# finalizer와 cleaner 사용을 피하라

- 자바는 finalizer와 cleaner 이 두가지 객체 소멸자를 제공한다.
<br>


---
## finalizer와 cleaner는 예측할 수 없고, 느리고 일반적으로 불필요하다.
  - finalizer는 오동작, 낮은성능, 이식성 문제의 원인이 된다.
  - cleaner는 finalizer의 대안으로서 나왔지만 여전히 예측할 수 없고 느리고 불필요하고 위험하다.
  - 자바의 소멸자는 C++의 파괴자와는 다른개념이다. 자바에서 자원회수역할은 GC가 담당하는게 바람직하다.
<br>


---
## finalizer와 cleaner는 즉시 수행된다는 보장이 없다.
  - finalizer와 cleaner는 제때 실행되어야 하는 작업은 절대 할 수 없다.
  - finalizer와 cleaner의 수행은 전적으로 GC 알고리즘에 달려있고, 이는 GC구현마다 천차만별이다.
<br>


---
## finalizer와 cleaner는 수행여부를 보장하지 않는다.
  - 접근할 수 없는 일부 객체에 딸린 종료작업을 전혀 수행하지 못한 채 프로그램이 중단될 수도 있다.
  - 프로그램 생애주기와 상관없는 상태를 영구적으로 수정하는 작업에는 finalizer나 cleaner에 절대 의존해선 안된다.
  - System.gc나 System.runFinalization 메소드는 finalizer와 cleaner가 실행될 가능성을 높여줄수는 있으나, 보장해주진 않는다.
<br>


---
## 심각한 성능문제를 동반한다.
  - finalizer는 GC의 효율을 50배 가까이 떨어뜨린다.
<br>


---
## 심각한 보안문제를 일으킬 수 있다.
```
   생성자나 직렬화과정에서 예외가 발생하면 이 생성되다 만 객체에서 악의적인 하위클래스의 finalizer가 수행될 수 있게된다.
   이 finalizer는 정적 필드에 자신의 참조를 할당하여 GC가 수집하지 못하게 막을 수 있다.
   이렇게 일그러진 객체가 만들어지고나면 , 이 객체의 메서드를 호출해 애초에는 허용되지 않았을 작업을 수행하는것은 일도 아니다.
  ```
  - 객체에서 생성을 막으려면 생성자에서 예외를 던지는것만으로 충분하지만, finalizer가 있다면 그렇지도 않다.
  ```
  final 클래스들은 그 누구도 하위클래스를 만들 수 없으니 이 공격에서 안전하다.
  final이 아닌 클래스를 finalizer공격으로부터 방어하려면
  아무 일도 하지않는 finalize 메서드를 만들고 final로 선언하자.
  ```
<br>


---
## AutoCloseable
  - 파일이나 스레드 등을 종료해야 할 자원을 담고있는 객체의 클래스에서 finalizer나 cleaner를 대신하는방법
  ```
  AutoCloseable을 구현해주고 클라이언트에서 인스턴스를 다 쓰고나면 close메서드를 호출해준다.
  ```
<br>


---
## cleaner를 안전망으로 활용하는 AutoCloseable 클래스 예제
```java
    import java.lang.ref.Cleaner;  
      
    public class Room implements AutoCloseable {  
      
	      private static final Cleaner cleaner = Cleaner.create();  
	      
	      private static class State implements Runnable {  
	      int numJunkpiles;  
	      
	      State(int numJunkpiles) {  
		      this.numJunkpiles = numJunkpiles;  
	      }  
	      
	      @Override  
	      public void run() {  
		      System.out.println("방 청소");  
		      numJunkpiles = 0;  
	      }  
	     }  
	     private final State state;  
	     private final Cleaner.Cleanable cleanable;  
	      
	     public Room(int numJunkpiles) {  
	      state = new State(numJunkpiles);  
	      cleanable = cleaner.register(this, state);  
	      }  
	      
	      @Override  
	      public void close() throws Exception {  
	      cleanable.clean();  
	      }  
    }

    public class main {  
      public static void main(String[] args) throws Exception {  
	      try (Room myRoom = new Room(7)) {
		      System.out.println("안녕~");
		  }
		  new Room(99);
		  System.out.println("아무렴~");
	  }
```
```
결과 : 

    안녕~
    방청소
    아무렴
```
<br>


---
## cleaner와 finalizer의 적절한 사용처
  - 자원의 소유자가 close메서드를 호출하지 않는 것에 대한 안전망 역할
  ```
  FileInputStream, FileOutputStream, ThreadPoolExecutor가 대표적인 예시이다.
  ```
  - 네이티브 피어와 연결된 객체
  ```
  네이티브 피어(native peer)는 일반 자바객체가 네이티브 메서드를 통해 기능을 위임한 네이티브  객체를 말한다.
  네이티브 피어는 자바객체가 아니니 GC는 그 존재를 알지 못하기때문에
  cleaner나 finalizer가 처리하기 적당한 작업이다.
  단 성능저하를 감당할 수 없거나 네이티브피어 자원을 즉시회수해야한다면 close메서드를 사용해야한다.
  ```
