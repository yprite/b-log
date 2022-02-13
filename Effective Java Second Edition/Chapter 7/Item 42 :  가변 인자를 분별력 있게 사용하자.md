자바 1.5 배포판엣 공식적을 가변 아리티 메소드라고 하는 가변 인자 메소드가 언어에 추가 됨
```
static int sum(int... args) {
  int sum = 0;
  for (int arg : args)
    sum += arg;
  return sum
}
```

sum(1,2,3)의 결과는 6이 될 것 이고, sum()의 결과는 0

```
static int min(int... args) {
  if (args.length == 0)
    throw new IllegalArgumentException("No args");
  int min = args[0];
  for (int i =1; i<args.length; i++)
    if (args[i] < min)
      min = args[i[;
    return min;
}
```
 위 코드의 문제느 아래와 같음
1. 클라이언트가 인자를 주지 않고 이 메소드를 호출하면 컴파일 시점이 아닌 런타임 시에 실행이 중단된다는 것
2. 타입이나 값의 범위가 적법한지 알기 위하 인자의 유효성 검사를 하는 코드를 명시적을 추가해야 함
3. min 지역 변수를 Integer.MAX_VALUE 값으로 초기화하지 않으면 for-each 루프문을 사용할 수 없음

앞 코드의 결함을 수정한 것은 아래와 같음
```
static int min(int firstArgs, int... remainintArgs) {
  int min = firstArgs;
  for (int arg : remainArgs) {
    if (arg < min)
      min = arg;
  return min;
}
```


- final 배열 매개 변수를 갖는 메소드라고 해서 모두 다 가변 인자로 개조하지는 말자.
- 연속된 값들이 가변적인 길이를 갖는 매개 변수로 메소드 호출이 필요할 때만 가변 인자를 사용하자

가변 인자 메소드는 가변적인 개수의 인자를 필요로 하는 메소드를 정의하는 편리한 방법이지만 절대로 남용해서는 안된다.
부적합하게 사용하면 혼란스러운 결과를 초래할 수 있기 때문
