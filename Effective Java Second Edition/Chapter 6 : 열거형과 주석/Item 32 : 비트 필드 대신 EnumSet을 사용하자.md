
```
public class Text {
    public static final int STYLE_BOLD = 1 << 0;            // 1
    public static final int STYLE_ITALIC = 1 << 1;          // 2
    public static final int STYLE_UNDERLINE = 1 << 2;       // 4
    public static final int STYLE_STRIKETHROUGH = 1 << 3;   // 8

    // 이 함수의 인자는 STYLE_상수를 비트별(bitwise) OR 한 값이거나 0.
    public void applyStyles(int styles) { ... }
}

//use
public static void main(String[] args){
    Text text = new Text();
    // 비트 필드 이제는 피해야 하는 구현법
    text.applyStyles(Text.STYLE_BOLD | Text.STYLE_ITALIC);
}
```

# 장점
 * 비트필드를 이용하면 합집합이나 교집합 같은 집합 연산을 비트 연산자를 사용해서 효율적으로 수행할 수 있음

# 단점
 * int enum 상수의 모든 단점을 갖음
 * 출력한 결과 값에 대해 이해하기 어려움
 * 비트필드로 표현된 모든 요소를 차례대로 반복해서 처리할 수 있는 방법이 없음
 

# EnumSet을 사용하자

 * 다른 Set구현들과 같은 수준의 상호운용성(interoperability)를 제공한다.
 * enum값 갯수가 64이하인 경우, 내부적으로 비트 백터(bit vector)를 사용하기 때문에 데이터 저장 효율도 좋다.
 * EnumSet은 long값 하나만 사용한다. 그렇기 때문에 비트 필드에 필적하는 성능이 나온다.


# 결론
 enum 타입이 단지 비트 집합에 사용된다는 것 때문에 그것을 비트 필드로 나타내야 할 이유는 없다
