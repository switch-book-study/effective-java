## 지역변수의 범위를 최소화하라
  - 지역변수의 유효범위를 최소로 줄이면 코드 가독성과 유지보수성이 높아지고 오류 가능성은 낮아진다.
  - 지역변수의 범위를 가장 효과적인 방법은 '가장 처음 쓰일 때 선언하기' 이다.
   ```
   레거시 코드의 c 언어 예시처럼, 지역변수를 코드 블록의 첫 머리에 미리 선언하는 경우
   코드가 어수선해져 가독성이 떨어진다.
   ```
  - 모든 지역변수는 선언과 동시에 초기화해야한다.
  - 메서드를 작게 유지하고 한가지 기능에 집중하는것도 지역변수의 범위를 최소화 하는 방법 중 하나이다.
