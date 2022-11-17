- 불변클래스란? 인스턴스 내부값을 수정할 수 없는 클래스, 객체가 파괴되는 순간까지 절대 달라지지 않는다.

- 불변클래스는 가변클래스보다
- 설계하고 구현하고 사용하기 쉽다
- 오류가 생길 여지가 적고 안전하다.

---
<br>


```
클래스를 불변으로 만드는 다섯가지 규칙

1. 객체의 상태를 변경하는 메서드(변경자)를 제공하지 않는다.
2. 클래스를 확장할 수 없도록 한다. (대표적으로 final 클래스가 있다.)
3. 모든 필드를 final로 선언한다.
  - 시스템이 강제하는 수단을 이용해 설계자의 의도를 명확히 드러낸다.
4. 모든 필드를 private으로 선언한다.
5. 자신 외에는 내부의 가변 컴포는트에 접근할 수 없도록 한다.
```
---
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

---
<br>
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

// 바깥에서 볼 수 없는 package-private 구현클래스를 원하는 만큼 만들어 활용할 수 있으니 훨씬 유연하다.
// 패키지 바깥의 클라이언트에서 바라본 이 불변객체는 사실상 final이다.
// public이나 protected생성자가 없으니 다른 패키지에서는 이 클래스를 확장하는게 불가능하기 때문이다.
```
---
<br>
```
- 클래스는 꼭 필요한 경우가 아니라면 불변이어야 한다.
- 성능때문에 어쩔 수 없다면 불변클래스와 쌍을 이루는 가변 동반클래스를 public클래스로 제공하도록 하자
- 불변으로 만들 수 없는 클래스라도 변경할 수 있는 부분을 최소한으로 줄이자.
- 객체가 가질 수 있는 상태의 수를 줄이면 그 객체를 예측하기 쉬워지고 오류가 생길 가능성이 줄어든다.
- 다른 합당한 이유가 없다면 모든필드는 private final이어야 한다.
- 생성자는 불변식 설정이 모두 완료된, 초기화가 완벽히 끝난 상태의 객체를 생성해야 한다.
- 정적팩터리 외에는 그 어떤 초기화메서드도 public으로 제공해서는 안된다.
```


