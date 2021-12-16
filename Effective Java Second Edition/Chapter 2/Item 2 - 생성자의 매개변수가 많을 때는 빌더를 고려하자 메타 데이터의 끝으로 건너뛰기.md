

Static 팩토리 메소드와 생성자는 공통적인 제약 존재

선택 가능한 매개변수가 많아질 경우 신축성 있게 처리하지 못함

예를 들어 포장식품에 붙은 영양 정보 라벨을 나타내는 클래의 경우 20개 이상의 필드가 존재(칼로리, 개수, 영양성분 ,,,,)

지금까지 대부분 프로그래머들은 텔리스코핑 생성자(Telescoping constructor) 패턴을 사용

즉, 필수 매개변수들과 선택 매개변수 두 개를 갖는 생성자 등의 형태로 모든 선택 매개변수를 생성자가 가질 수 있도록 여러 개의 생성자를 겹겹이 만듬

```
public class NutritionFacts {
    private final int servingSize;
    private final int servigs;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;
 
    public NutritionFacts(int servingSize, int servigs) {
        this(servingSize, servings, 0);
    }
    ....
}
```

위 클래스의 인스턴스를 생성할 때 모든 매개변수를 포함하는 생성자를 사용한다면 아래와 같음
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27);

일반적으로 이런 식의 생성자 호출은 우리가 원하지 않는 매개변수에도 초기값을 주어야 하며, 가독성도 떨어져 코드를 파악하는 사람의 입장에서 그런 모든 값들이 어떤 의미를 갖는지 의아한 상태에서 매개변수의 개수를 주의 깊게 세어봐야 함.


매개변수가 많은 생성자의 두 번째 대안으로 자바빈즈(JavaBeans) 패턴이 있음.

이  패턴에서는 매개변수가 없는 생성자를 호출해서 객체를 생성한 후 세터(setter) 메소드를 호출해서 각각의 필수 필드와 선택 필드 값을 지정한다.
```
public class NutritionFacts {
    private final int servingSize;
    private final int servigs;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;
 
    public NutritionFacts() {}
    public void setServingSize(int val) { servingSize = val; }
    public void setServings(int val) { servings = val; }
    public void setCalories(int val) { calories= val; }
 
    ....
}
```

이 패턴은 텔리스코핑 생성자 패턴과 같은 단점을 전혀 갖지 않으며, 가독성도 좋음

하지만 자바빈즈 패턴은 심각한 단점을 갖고 있음

여러 번의 메소드 호출로 나누어져 인스턴스가 생성되므로, 생성 과정을 거치는 동안 자바빈 객체가 일관된 상태를 유지하지 못할 수 있음

생성자 매개변수의 유효성을 검사하여 일관성을 유지하도록 하는 옵션조차도 클래스에 없기 때문임

자바빈즈 패턴은 불변 클래스를 만들 수 있는 가능성을 배제하므로 스레드에서 안정성을 유지하려면 프로그래머의 추가적인 노력이 필요하다는 단점이 존재


텔리스코핑 생성자 패턴의 안전성과 자바빈즈 패턴의 가독성을 결합한 세 번째 방법이 있다. 

빌더 패턴 (Builder Pattern)의 형태로서 원하는 객체를 바로 생성하는  대신 클라이언트는 모든 필수 매개변수를 갖는 생성자를 호출하여 빌더 객체를 얻음
