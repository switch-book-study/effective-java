## 리플렉션보다는 인터페이스를 사용하라.
  - 리플렉션 이용 시
    - 컴파일타임 타입 검사가 주는 이점을 하나도 누릴 수 없다.
    - 코드가 지저분해지고 장황해진다.
    - 성능이 떨어진다.

  - 리플렉션은 아주 제한된 형태로만 사용해야 그 단점을 피하고 이점만 취할 수 있다.
  - 리플렉션은 인스턴스 생성에만 쓰고, 이렇게 만든 인스턴스는 인터페이스나 상위 클래스로 참조해 사용하자.
  ```java
  //리플렉션으로 생성하고 인터페이스로 참조해 활용한다.
  public static void main(String[] args) {
    //클래스 이름을 Class객체로 변환
    Class<? extends Set<String>> cl = null;
    try {
      cl = (Class<? extends Set<String>>) //비검사 형변환
        Class.forName(args[0]);
      } catch(ClassNotFoundException e) {
        fatalError("클래스를 찾을 수 없습니다.");
      }
      
      //생성자를 얻는다.
      Constructor<? extends Set<String>> cons = null;
      try{
        cons = cl.getDeclaredConstructor();
      } catch (NoSuchMethodException e) {
        fatalError("매개변수 없는 생성자를 찾을 수 없습니다.");
      }
      
      //집합의 인스턴스를 만든다.
      Set<String> s = null;
      try {
        s = cons.newInstance();
      } catch (IllegalAccessException e) {
        fatalError("생성자에 접근할 수 없습니다.");
      } catch (InstantiationException e) {
        fatalError("클래스를 인스턴스화 할 수 없습니다.");
      } catch (InvocationTargetException e) {
        fatalError("생성자가 예외를 던졌습니다" + e.getCause());
      } catch (ClassCastException e) {
        fatalError("Set을 구현하지 않은 클래스입니다.");
      }
      
      //생성한 집합을 사용한다.
      s.addAll(Arrays.asList(args).subList(1, args.length));
      System.out.println(s);
    }
    
    private static void fatalError(String msg) {
      System.err.println(msg);
      Systtem.exit(1);
    }
  ```
  
  ```
  리플렉션은 복잡한 특수 시스템을 개발할 때 필요한 강력한 기능이지만 단점도 많다.
  컴파일타임에는 알 수 없는 클래스를 사용하는 프로그램을 작성한다면 리플렉션을 사용해야 할 것이다.
  단, 되도록 객체생성에만 사용하고, 생성한 객체를 이용할 때는 적절한 인터페이스나 컴파일타임에 알 수 있는 상위 클래스로 형변환해 사용해야한다.
  ```
