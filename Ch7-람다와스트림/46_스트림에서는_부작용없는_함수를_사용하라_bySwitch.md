## 스트림에서는 부작용없는 함수를 사용하라.
  - 스트림은 `함수형 프로그래밍`에 기초한 패러다임이다.
  - 핵심은 계산을 일련의 `변환`으로 재구성하는 부분
  -` 각 변환단계`는 가능한 한 이전단계의 결과를 받아 처리하는 `순수함수` 여야한다.
  - 순수함수란?
     ```
     오직 입력만이 결과에 영향을 주는 함수를 말한다.
     다른 가변상태를 참조하지 않고 
     함수 스스로도 다른 상태를 변경하지 않는다.
     ```
  - `스트림 연산`에 건네는 함수 객체는 모두 `side effect`가 없어야 한다.
  - 스트림 코드를 가장한 반복적 코드는 길고, 읽기어렵고, 유지보수에 좋지않다.
  ```
  for-each문은 종단 연산 중 기능이 가장 적고 가장 '덜' 스트림스럽다.
  대놓고 반복적이라 병렬화할 수도 없다.
  forEach연산은 스트림 계산결과를 보고할 때만 사용하고, 계산하는 데는 쓰지말자.
  ```
  
  
## 스트림의 collector
   ```java
   // 빈도표에서 가장 흔한 단어 10개를 뽑아내는 파이프라인
   List<String> topTen = freq.keySet().stream()
         .sorted(comparing(freq::get).reversed())
         .limit(10)
         .collect(toList());
   ```
   - 마지막 toList()는 Collectors의 메서드다. 이처럼 Collectors의 멤버를 정적 임포트하여 쓰면 스트림 파이프라인 가독성이 좋아져서 흔히 이렇게 쓴다.

## Collectors의 메서드를 활용한 스트림 예시
  - toMap수집기를 사용하여 문자열을 열거 타입 상수에 매핑한다.
  ```java
  priavate static final Map<String, Iperation> stringToEnum =
    Stream.of(value()).collect(
      toMap(Object::toString, e-> e));
  ```
  
