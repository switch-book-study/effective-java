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
  
