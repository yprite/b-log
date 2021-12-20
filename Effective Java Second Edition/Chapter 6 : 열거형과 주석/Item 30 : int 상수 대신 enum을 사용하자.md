
열겨형은 적법한 값을 각즌 정해진 개수의 상수들로 구성되는 타입

```
public static final int APPLE_FUJI			= 0;
public static final int APPLE_PIPPIN		= 1;
public static final int APPLE_GRANNY_SMITH	= 2;

public static final int ORANGE_NAVEL		= 0;
public static final int ORANGE_TEMPLE		= 1;
public static final int ORANGE_BLOOD		= 2;
```

위의 예는 int enum 패턴이며, 많은 단점이 있음

* 타입 안전을 보장하는 방법이나 편리하게 사용할 수 있는 방법을 제공하지 않음
	+ int enum 패턴을 사용하는 프로그램은 취약 - 컴파일 시점의 상수
	+ int enum  상수를 출력 가능한 문자열로 쉽게 바꾸는 방법도 없음
	+ 이 패턴의 변이로서 String enum  패턴이 있음
		- 문자열 비교에 의존하므로 성능의 문제가 생길 수 있음
		- 필드명 대신에 String 상수 값을 클라리언트 코드에 하드코드 할 수 있다는 것

자바의 enum 타입을 사용할 때

장점
	* enum 자료형은 final로 선언된 것과 같음
	* enum 자료형은 새로운 객체를 생성하거나 계승을 통해 확장할 수 없기 때문에 이미 선언된 enum상수이외의 객체는 사용할수 없음
	* 이름 공간이(namespace)이 분리되기 때문에 다른 이름의 enum상수를 인자로 넘기거나 ==연산을 시도하면 컴파일 에러가 발생한다. 상수를 추가하거나 순서를 변경해도 클라이언트에서는 다시 컴파일을 할 필요가 없다. 왜냐하면, 상수를 제공하는 필드가 enum 자료형과 클라이언트 사이에 격리 계층(layer of insulation) 구실을 하기 때문이다.
	* toString함수를 호출하면 인쇄 가능 문자열로 쉽게 변환 가능함
	* enum은 단순한 자료형에서 그치지 않고, 임의의 함수나 필드도 추가 가능함, 그렇기 때문에 임의의 인터페이스를 구현할수도 있음
	* enum상수의 직렬화 형식(serialized form)은 enum자료형상의 변화 대부분을 견딜수 있도록 설계되어 있음
	* 비교(Comparable), 직렬화(Serializable), Object 함수 재정의 가능
	* 일반 객체처럼 상태와 행위를 가질수 있으며, 이것을 풍부하게 표현할 수 있다. 거기에다 불편성(immutable)을 보장한다.

```
public enum Operation{
    PLUS, MINUS, TIMES, DIVIDE;
    double apply (double x, double y){
        switch(this){
            case PLUS:      return x + y;
            case MINUS:     return x - y;
            case TIMES:     return x * y;
            case DIVIDE:    return x / y;
        }
        throw new AssertionError("Unknow op: " + this);
    }
}
```

enum 자료형이 늘어 날때 마다 switch 문도 같이 고쳐야 함.

좋은 방법은 enum자료형에 abstract double apply(double x, double y); 선언하고, 각 상수별 클래스 몸체(constant-specific class body)안에서 실제 함수를 재정하는 것

```
public enum Operation {
    PLUS   {double apply(double x, double y) {return x + y;}},
    MINUS  {double apply(double x, double y) {return x - y;}},
    TIMES  {double apply(double x, double y) {return x * y;}},
    DIVIDE {double apply(double x, double y) {return x / y;}};

    abstract double apply(double x, double y);
}
```

상수별로 함수 구현은 상수별 데이터와 혼동될수 있기 때문에 아래와 같이 toString을 재정의하여 기호를 반환

```
public enum Operation {
    PLUS("+")   {double apply(double x, double y) {return x + y;}},
    MINUS("-")  {double apply(double x, double y) {return x - y;}},
    TIMES("*")  {double apply(double x, double y) {return x * y;}},
    DIVIDE("/") {double apply(double x, double y) {return x / y;}};

    private final String symbol;

    Operation(String symbol){
        this.symbol = symbol;
    }

    @Override
    public String toString(){
        return symbol;
    }

    abstract double apply(double x, double y);
}

public static void main(String[] args){
    double x = 10; // Double.parseDouble(args[0]);
    double y = 20; // Double.parseDouble(args[1]);
    Arrays.stream(Operation.values())
            .forEach(op->
                    System.out.printf("%f %s %f = %f%n",x, op, y, op.apply(x,y)));
}
```

중복되는 행위(정책)이 필요한 경우, 아래처럼 하위 정책 enum에 위임해서(전략 enum(strategy enum)) 다형성과 재사용성을 확보가능

```
enum PayrollDay {
    MONDAY(PayType.WEEKDAY),    TUESDAY(PayType.WEEKDAY),
    WEDNESDAY(PayType.WEEKDAY), THURSDAY(PayType.WEEKDAY),
    FRIDAY(PayType.WEEKDAY),    SATURDAY(PayType.WEEKDAY),
    SUNDAY(PayType.WEEKEND);

    private final PayType payType;
    PayroleDay(PayType payType) { this.payType = payType; }

    double pay(double hoursWorked, double payRate) {
        return payType.pay(hoursWorked, payRate);
    }
    // 정책 enum 자료형
    private enum PayType {
        WEEKDAY {
            double overtimePay(double hours, double payRate) {
                return hours <= HOURS_PER_SHIFT ? 0 :
                    (hours - HOURS_PER_SHIFT) * payRate / 2;
            }
        },
        WEEKEND {
            double overtimePay(double hours, double payRate) {
                return hours * payRate / 2;
            }
        };
        private static final int HOURS_PER_SHIFT = 8;

        abstract double overtimePay(double hrs, double payRate);

        double pay(double hoursWorked, double payRate) {
            double basePay = hoursWorked * payRate;
            return basePay + overtimePay(hoursWorked, payRate);
        }
    }
}
```

# 결론
	* enum은 int 상수와 성능면에서 비등하다.(자료형을 메모리에 올리고 초기화하는 공간적/비용적 비용 때문에 약간 손해를 보긴 한다.)
	* int 상수보다 기능적, 안정성 등에서 enum자료형을 사용하는 것이 더 좋다.
	* 속성과 행위를 추가할수 있기 때문에 int형 자료 보다 더욱 풍부하게 모델링 할수 있다.
	* 분기(if, switch)대신 상수별 함수로 구현하라.
	* 상수 별로 공통 기능이 요구 되면 전략 enum패턴(strategy enum)을 고려 하라.




