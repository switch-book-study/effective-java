- 불변클래스란? 인스턴스 내부값을 수정할 수 없는 클래스, 객체가 파괴되는 순간까지 절대 달라지지 않는다.

- 불변클래스는 가변클래스보다
- 설계하고 구현하고 사용하기 쉽다
- 오류가 생길 여지가 적고 안전하다.

```
클래스를 불변으로 만드는 다섯가지 규칙

1. 객체의 상태를 변경하는 메서드(변경자)를 제공하지 않는다.
2. 클래스를 확장할 수 없도록 한다. (대표적으로 final 클래스가 있다.)
3. 모든 필드를 final로 선언한다.
  - 시스템이 강제하는 수단을 이용해 설계자의 의도를 명확히 드러낸다.
4. 모든 필드를 private으로 선언한다.
5. 자신 외에는 내부의 가변 컴포는트에 접근할 수 없도록 한다.
```

```java
//불변 복소수 클래스 예제
public final class Complex {
  private final double re;
  private final double im;
  
  public double realPart() { return re; }
  public double imaginaryPart() { return im; }
  
  public Complex plus(Complex c) {
    return new Complex(re + c.re, im + c.im);
  }
  
  ...
  
}

//예제에서 사칙연산 메서드들이 인스턴스 자신은 수정하지 않고
//새로운 Complex 인스턴스를 만들어 반환해준다.
```

- 불변객체는 단순하며 생성된 시점의 상태를 파괴될때까지 그대로 간직한다.
- 불변객체는 근본적으로 스레드 안전하여 따로 동기화할 필요가 없다.
- 불변객체에 대해 어떤 스레드도 다른스레드에 영향을 줄 수 없으니 안심하고 공유할 수 있다.
- 불변객체는 그 자체로 실패원자성을 제공한다.
- 단 불변클래스는 값이 다르면 반드시 독립된 객체로 만들어야하는 단점이 있다.


```java
// 생성자 대신 정적 팩터리를 사용한 불변클래스 예제
public class Complex {
  private final double re;
  private final double im;
  
  private Complex(double re, double im) {
    this.re = re;
    this.im = im;
  }
  
  public static Complex valueOf(double re, double im) {
    return new Complex(re, im);
  }
  
  ...
}

// 
```

