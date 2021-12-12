

클라이언트가 클래스의 인스턴스를 얻는 수단은 public 생성자 이다.

하지만 프로그래머가 알아 둬야 할 기법이 하나 있는데 그것이 정적 팩토리 매소드 패턴이다.


장점 1 : 이름을 가질 수 있다.
```
public class Human {
 
    private String name;
     
    public Human(String name) {
        this.name = name;
    }
 
    public String getName() {
        return name;
    }
     
}
```



위 클래스에서 인스턴스를 얻는 수단은 생성자를 통해 얻을 수 있다.

```
public class Test {
     
    public static void main(String[] args) {
         
        Human zolla = new Human("zolla");
        System.out.println(zolla.getName());
         
        Human zola = new Human("zola");
        System.out.println(zola.getName());
    }
 
}
```


여기서 정적 팩토리 메소드를 통해 클래스가 이름을 가질 수 있는데,
```
public class Human {
 
    private String name;
     
    private Human(String name) {
        this.name = name;
    }
 
    public String getName() {
        return name;
    }
     
    public static Human createZolla() {
        return new Human("zolla");
    }
     
    public static Human createZola() {
        return new Human("zola");
    }
}
```

아래처럼 호출하면 된다.
```
public class Test {
     
    public static void main(String[] args) {
         
        Human zolla = Human.createZolla();
        System.out.println(zolla.getName());
         
        Human zola = Human.createZola();
        System.out.println(zola.getName());
    }
 
}
```



장점 2 : 호출될 때 마다 인스턴스를 새로 생성하지 않아도 된다.
```
public final class Boolean implements java.io.Serializable,
                                      Comparable<Boolean>
{
    /**
     * The {@code Boolean} object corresponding to the primitive
     * value {@code true}.
     */
    public static final Boolean TRUE = new Boolean(true);
 
    /**
     * The {@code Boolean} object corresponding to the primitive
     * value {@code false}.
     */
    public static final Boolean FALSE = new Boolean(false);
 
    .......
}
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

위를 참고하면 valueOf 메소드인데 Boolean.TRUE/Boolean.FALSE 객체를 상수로 선언 해서 아래의 valueOf 메소드에서 활용하는 것 그렇게 되므로 불필요하게 낭비되는 객체를 줄일 수 있고 이것이 Flyweight 패턴(Flyweight pattern)과 비슷하다고 할 수 있다.
정적 팩토리 메소드 방식은 언제 어느 인스턴스가 살아 있게 할지를 철저히 통제할 수 있다. 이런 클래스를 인스턴스 통제(instance-cotrolled) 클래스라고 한다.

인스턴스의 통제 이유

    클래스를 싱글톤으로 만들수 있다.
    인스턴스화 불가로 만들 수 있다.
    불변 값 클래스에서 동치인 인스턴스가 단 하나뿐임을 보장할수 있다(a.equals(b))

인스턴스 통제는 플라이웨이트 패턴(Flyweight pattern) 근간이 되면 열거 타입은 인스턴스가 하나가 만들어 짐을 보장함



장점 3 : 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.

이것은 반환할 객체의 구현을 맘대로 선택할 수 있는 장점이 있다.
API를 만들 때 이 유연성을 응용하면 구현 클래스를 공개하지 않고도 그 객체를 반환 할 수 있어서 API를 작게 유지 할 수 있다.
이는 인터페이스를 정적 팩터리 메서드의 반환 타입으로 사용하는 인터페이스 기반 프레임워크를 만드는 핵심기술이다.

아래는 java.util.Collections 의 일부 코드 발췌이다.
```
public static <E> List<E> checkedList(List<E> list, Class<E> type) {
      return (list instanceof RandomAccess ?
              new CheckedRandomAccessList<>(list, type) :
              new CheckedList<>(list, type));
  }
```

위에서 보면 checkedList 메소드는 인터페이스인 List를 반환 하지만 구현체는 아래에서 CheckedRandomAccessList인지 CheckedList 인지를 선택해서 반환하게 된다.

그리고 저기 List에 구현체인 CheckedRandomAccessList, CheckedList는 외부에 공개 되지 않고 단 하나인 외부 구현체인 Collections를 통해서만 얻을 수 있게 했다.
The Collections Framework는 공개하지 않는 클래스 덕분에 API 외형을 줄일 수 도 있고 프로그래머가 알아야 할 클래스를 줄여 줄 수도 있었다.


장점 4: 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환 할 수 있다.
```
EnumSet클래스는 정적 팩토리 메소드 패턴으로만 제공하는데
public static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> elementType) {
       Enum<?>[] universe = getUniverse(elementType);
       if (universe == null)
           throw new ClassCastException(elementType + " not an enum");
 
       if (universe.length <= 64)
           return new RegularEnumSet<>(elementType, universe);
       else
           return new JumboEnumSet<>(elementType, universe);
   }
```

위 noneOf 메소드를 보면 인자의 원소가 64개 이하면 RegularEnumSet을 반환하고 65개 이상이면 JumboEnumSet을 반환한다.
이런 방법은 버전에 따라서 다른 클래스를 반환해도 문제가 없고 심지어 다음 버전에서 RegularEnumSet을 삭제해도 시스템에 문제가 없다(느슨한 결합)



장점 5 : 정적 팩터리 매서드를 작성하는 시점에는 반환할 객체의 클래스가 존재 하지 않아도 된다.

JDBC에서 커넥션을 가져오는 코드는 다음과 같다.
```
Class.forName("oracle.jdbc.driver.OracleDriver");
Connection con = DriverManager.getConnection("jdbc:oracle:@localhost:8080", "ddd", "ddd");
```

여기서 getConnection()에 의해 반환되는 구현체는 DBMS의 종류에 따라 달라지게 된다. 정적 팩토리 메서드를 이용하면 각 DBMS에 맞는 API를 따로 구현하지 않고 클래스가 로드되는 시점에서 구현체를 바꿔치기 할 수 있다.
```
public class DriverManager {
    private DriverManager() {}
 
    public static Connection getConnection(String name) {
        Driver driver = new Driver("default driver name");
 
        // 어떤 약속된 텍스트 파일에서 Driver 구현체의 FQCN을 읽어온다.
        // FQCN에 해당하는 인스턴스를 생성한다.
        // diver 변수가 해당 인스턴스를 참조하도록 한다(바꿔치기 한다).
        // ex) driver = new Driver(name);
 
        return driver;
    }
}
```



단점 1 : 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩토리 메서드만 제공하면 하위 클래스를 만들 수 없다.
예를 들어 java.util.Collections는 private 생성자만 있기 때문에 상속을 할 수 없다.
이 제약은 상속보다 컴포지션을 사용하도록 유도하고 불변 타입으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들일 수도 있다. 

Composition


단점 2 :  정적 팩토리 메서드는 프로그래머가 찾기 어렵다.

javadoc이 생성자는 알아서 위에다가 정리해주는데 정적 팩토리 메서드에는 그런걸 안해준다.
따라서 API 문서를 잘 작성하고 널리 알려진 메서드 네이밍 컨벤션을 사용해서 클라이언트가 잘 사용할 수 있게 해줘야한다(이름을 잘 짓자!).


다음은 정적 팩토리 메서드에 흔히 사용하는 명명 방식들이다.

from : 매개 변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드
```
Date d = Date.from(instance);
```

of : 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드
```
Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
```


valueOf : from과 of의 더 자세한 버전
```
BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE)
Integer integer = Integer.valueOf("35");
```

instance 혹은 getInstance : (매개변수를 받는다면) 매개변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지는 않는다.
```
StackWalker luke = StackWalker.getInstance(options);
```

create 혹은 newInstance : instance 혹은 getInstance와 같지만, 매번 새로운 인스턴스가 보장됨을 반환한다.
get_Type_ : getInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩토리 메서드를 정의할 때 쓴다. "Type"은 팩토리 메서드가 반환할 객체의 타입이다.
```
FileStore fs = Files.getFileStore(path);
```

new_Type_ : newInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩토리 메서드를 정의할 때 쓴다. "Type"은 팩토리 메서드가 반환할 객체의 타입이다.
```
BufferedReader br = Files.newBufferedReader(path);
```

type : get_Type_과 new_Type_의 간결한 버전
```
List<Complaint> litany = Collections.list(legacyLitany);
```





```
package com.sec.scloud.storage.notestacker.common.utils;
 
import com.sec.service.logger.SCloudLoggerFactory;
 
public class NoteStackerLoggerFactory {
 
    public static NoteStackerLogger getLogger(String name) {
        return new NoteStackerLogger(SCloudLoggerFactory.getLogger(name));
    }
 
    public static NoteStackerLogger getLogger(Class<?> clazz) {
        return getLogger(clazz.getName());
    }
     
}
```


