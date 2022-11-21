## 자바의 다중 구현 메커니즘
  1. 추상 클래스
  2. 인터페이스
  - 자바는 단일 상속만 지원한다.

##
  - 인터페이스는 `믹스인` 정의에 안성맞춤이다.
  - Coimparable
   - 자신을 구현한 클래스의 인스턴스들 끼리는 순서를 정할 수 있다고 선언하는 믹스인 인터페이스

## 인터페이스로 계층구조가 없는 타입 프레임워크를 만들 수 있다.
  ```java
  public interface Singer {
    AudioClip sing(Song s);
  }
  public interface Songwriter {
    Song compose(int chartPosition);
  }
  
  public interface SingerSongwriter extends Singer, Songwriter {
    AudioClip strum();
    void actSensitive();
  }
  ```
  - 예제정도의 `유연성`이 항상 필요하지는 않지만, 이렇게 만들어둔 인터페이스가 결정적인 도움을 줄 수도 있다.
  - 같은구조를 클래스로 만드려면 가능한 조합 전부를 각각 정의한 `고도비만 계층구도`가 만들어질것이다.
  - 흔히 `조합폭발`이라 부르는 현상이다.
  - 래퍼클래스 관용구와 함께 사용하면 `인터페이스는 기능을 향상시키는 안전하고 강력한 수단`이 된다.


## 템플릿 메서드 패턴
  - 인터페이스와 추상골격구현 클래스를 함께 제공하는식으로 인터페이스와 추상클래스의 장점을 모두 취할 수 있다.
  - 인터페이스로는 타입을 정의하고 필요하면 디폴트 메서드 몇 개도 함께 제공한다.
  - 골격 구현 클래스는 나머지 메서드들까지 구현한다.
  - 골격 구현을 확장하는 것만으로 인터페이스를 구현하는 데 필요한 일이 대부분 완료된다.
  ```java
  //골격 구현을 사용해 완성한 구체 클래스
  static List<Integer> intArrayAsList(int[] a) {
    Object.requireNonNull(a);
    
    return new AbstractList<>() {
      @Override public Intreger ger(int i) {
        return a[i];  //오토박싱
      }
      
      @Override public Integer set(int i, Integer val) {
        int oldVal = a[i];
        a[i] = val; //오토언박싱
        return oldVal;  //오토박싱
      }
      
      @Override public int size() {
        return a.length;
      }
    };
  }
  ```
  
---
<br>

- 정리
```
일반적으로 다중 구현용 타입으로는 인터페이스가 가장 적합하다.
복잡한 인터페이스라면 구현하는 수고를 덜어주는 골격 구현을 함께 제공하는 방법을 꼭 고려해보자.
골격구현은 '가능한 한' 인터페이스의 디폴트메서드로 제공하여 그 인터페이스를 구현한 모든곳에서 활용하도록 하는것이 좋다.
인터페이스에 걸려있는 구현상의 제약때문에 골격구현을 추상클래스로 제공하는 경우가 더 흔하기 때문이다.
```
