생성자를 private 로 만들어서 해당 클래스 외부에서 따로 생성하지 못하도록 해야함

```
  public class Elvis {
    public static final Elvis INSTANCE = new Elvis(); // static final!!
    private ElvisO { ... } // private 생성자!!
    public void leaveTheBuilding() { .. . }
  }	
```

enum 싱글톤을 사용하는 이유?

enum 없이 싱글톤을 만들면 reflection 을 통해서는 instance 생성자에 접근할 수가 있다.

싱글톤에서 serializable 을 사용하려면 instance 변수는 transient 로 선언해야 한다. 매번 deserialize 할 때 마다 instance 에 새로운 값이 생성될 수 있으므로 transient 를 통해 serialize 할 때 제외하도록 설정해 주어야 한다.

java 1.5 이상을 사용하면 enum 을 통해서 싱글톤을 구현하면 좋다. 여러번 초기화 오브젝트가 생성되거나 serialization, reflection attack 등에 상관없이 구현 가능하다

```
public enum Elvis{
     INSTNACE;
     private String test = "abc"
     public void leaveTheBuilding(){
          this.test = "ccc"; // INSTANCE.test 도 가능.
     }
 }
```

enum 방식에 싱글톤은 널리 적용되어 있지 않다. 개인적으로도 Serialize 문제가 아니라면 구지 사용할 필요가 없다고 생각된다.
