## 가변인수는 신중히 사용하라
  - 가변인수 메서드는 명시한 타입의 인수를 0개 이상 받을 수 있다.
    - 가변인수 메서드를 호출하면 가장먼저 인수의 개수와 길이가 같은 배열을 만들고
    - 인수들을 이 배열에 저장하여 가변인수 메서드에 건네준다.
    ```java
    // 간단한 가변인수 활용의 예
    static int sum (int... args) {
      int sum = 0;
      for (int arg: args)
        sum += arg;
      return sum;
    }
    ```
    - 인수가 1개 이상이어야 할 때 가변인수를 제대로 사용하는 방법
    ```java
    static int min(int firstArg, int... remainingArgs) {
      int min = firstArg;
      for (int arg: remainingArgs)
        if (arg < min)
          min = arg;
      return min;
    ```
