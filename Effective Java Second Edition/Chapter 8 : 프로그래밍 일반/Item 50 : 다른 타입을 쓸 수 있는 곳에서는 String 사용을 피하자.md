String은 텍스트를 나타내기 위해 설계되었으나 본래의 설계 취지와는 다른 목적으로 사용하는 경향이 있음

### String으로 다른 값 타입을 대체하는 것은 좋지 않음
- 파일, 네트워크, 키보드 입력으로부터 데이터가 프로그램으로 전달될 때 문자열 형식인 경우가 많으며 그대로 두려는 경향
- 실제로 데이터가 원문 그대로일 때만 옳음
- 데이터가 숫자라면 int, float, BigInteger와 같이 적합한 숫자 타입으로 변환

### String으로 enum 타입을 대체하는 것은 좋지 않음
 - enum 타입은 String보다 훨씬 더 좋은 열거형 상수를 만들어야 됨

### String으로 집합(Aggregate) 타입을 대체하는 것은 좋지 않음
- String compoundKey = className + "#" + i.next(); -> String을 집합 타입에 부적절하게 사용한 예 

### String으로 역량을 대체하는 것은 좋지 않음
```
public class ThreadLocal {
    private ThreadLocal() {}
    public static void set(String key, Object value);
    public static Object get(String key);
}
```
- 스레드 지역 변수의 네임 스페이스를 나타내는 문자열 값으로 된 키가 여러 스레드 간에 전역적으로 공유된다는 것
- 위의 API 코드는 문자열을 위조 불가능한 키로 변경하여 문제를 해결할 수 있음

요약
- 더 좋은 데이터 타입이 있거나 또는 작성할 수 있다면, 객체를 String으로 표한하는 경향을 피하자
- String을 부적합하게 사용하면, 다른 타입에 비해 더 번거롭고 유연성이 떨어지며, 속도도 더 느려지고 에러가능성이 커짐
- 일반적으로 String으로 잘못 사용하는 타입은 기본형 데이터 타입, enum, 집합 타입들임
- 
