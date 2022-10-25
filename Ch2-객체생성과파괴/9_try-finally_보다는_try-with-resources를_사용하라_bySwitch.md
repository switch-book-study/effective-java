## java에서 자원 관리
  - java라이브러리에는 close 메서드를 호출해 직접 닫아줘야하는 자원이 많다. (ex InputStream, OutputStream, java.sql.Connection 등)
  - 자원 닫기는클라이언트가 놓치기 쉬워서 예측할 수 없는 성능문제로 이어지기도 한다.
  - 이런 자원 중 상당수가 안전망으로 finalizer를 활용하고는 있지만 그리 신뢰할만하지 않다.


## 자원 닫힘을 보장하는 수단 try-finally
  - try-finally는 자원을 회수하는 방책 중 하나였으나 더이상 권장되지않는다.
  ```java
  static String firstLineOfFile(String path) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader(path));
    try {
      return br.readLine();
    } finally {
      br.close();
    }
  }
  ```
  여기서 만약 자원을 하나 더 사용한다면 ? 매우 지저분한 코드가 된다.
  ```java
  static void copy(String src, String dst) throws IOException {
    InputStream in = new FileInputStream(src);
    try {
      OutputStream out = new FileOutputStream(dst);
      try {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while ((n = in.read(buf)) >= 0)
          out.write(buf, 0, n);
      } finally {
        out.close();
      }
    } finally {
      in.close();
    }
  }
  ```
  ```
  예외는 try블록과 finally 블록 모두에서 발생할 수 있는데,
  firstLineOfFile메서드 안의 readLine메서드가 예외를 던지고 같은이유로 close 메서드도 실패할 가능성이 있다.
  이런경우 두번째 예외가 첫번째 예외를 완전히 집어삼켜서
  스택추적 내역에 첫번째 예외에 관한 정보는 남지않게되어 디버깅을 어렵게한다.
  ```

## try-with-resources를 통한 문제해결
 - 이 구조를 사용하려면 해당 자원이 AutoCloseable 인터페이스를 구현해야한다.
 - 많은 자바 라이브러리와 서드파티 라이브러리들의 클래스와 인터페이스는 이미 AutoCloseable을 구현하거나 확장해뒀다.
 ```java
 //try-with-resources
 static String firstLineOfFile(String path) throw IOException {
  try (BufferedReader br = new BufferedReader(
    new FileREader(path))) {
    return br.readLine();
    }
  }
  ```
  - 복수의 자원처리도 try-with-resources를 적용해서 문제해결 할 수 있다.
  ```java
  static void copy(String src, String dst) throw IOException {
    try (InputStream in = new FileInputStream(src);
      OutputStream out = new FileOutputStream(dst)) {
      byte[] buf = new byte[BUFFER_SIZE];
      int n;
      while((n = in.read(buf)) >= 0)
        out.write(buf, 0, n);
      }
   }
   ```
   - try-with-resources를 적용하면 짧고 읽기 수월할 뿐 아니라 디버깅도 쉬워진다.


```
정리.
회수해야하는 자원을 다룰때는 try-finally 말고, try-with-resources를 사용하자
코드는 짧고 분명해지고 예외정보도 직관적이게된다.
```
