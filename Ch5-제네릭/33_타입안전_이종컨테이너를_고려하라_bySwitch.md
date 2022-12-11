## 타입 안전 이종 컨테이너를 고려하라
  - 제네릭은 컬렉션, 단일원소 컨테이너에 흔히 쓰인다.
  - 이런 모든 쓰임에서 매개변수화되는 대상은 컨테이너 자신이다.
  - 따라서 하나의 컨테이너에서 매개변수화할 수 있는 타입의 수가 제한된다.

## 타입 안전 이종 컨테이너 패턴 (type safe heterogeneous container pattern)
  ```java
  //타입 안전 이종 컨테이너 패턴 - API
  public class Favorites {
    public <T> void putFavorite(Class<T> type, T instance);
    public <T> T getFavorite(Class<T> type);
  }
  ```
  ```java
  //타입 안전 이종 컨테이너 패턴 - 클라이언트
  public static void main(String[] args) {
    Favorites f = new Favorites();
    
    f.putFavorite(String.class, "Java");
    f.putFavorite(Integer.class, 0xcafebabe);
    f.putFavorite(Class.class, Favorites.class);
    
    String favoriteString = f.getFavorite(String.class);
    int favoriteInteger = f.getFavorite(Integer.class);
    Class<?> favoriteClass = f.getFavorite(Class.class);
    
    System.out.printf("%s %x %s%n", favoriteString, favoriteInteger, favoriteClass.getName());
  }
  ```
  - Favorites 인스턴스는 타입안전하다.
  - 또한 모든 키의 타입이 제각각이라 일반적인 맵과 달리 여러 가지 타입의 원소를 담을 수 있다.
  ```java
  // 타입 안전 이종 컨테이너 패턴 - 구현
  public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();
    
    public <T> void putFavorite(Class<T> type, T instance) {
      favorites.put(Objects.requireNonNull(type), instance);
    }
    
    public <T> getFavorite(Class<T> type) {
      return type.cast(favorites.get(type));
    }
  }
  ```
