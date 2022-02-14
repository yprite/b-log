```
private final List<cheese> cheeseInStock =  ....;

public Cheese[] getCheeses() {
    if (cheeseInStock.size() == 0)
        return null;
    ...
}
```
판매할 치즈가 하나도 없는 상황에서 null 반환 값을 처리하기 위해 다음과 같이 클라이언트 코드가 추가 됨
```
Cheese[] cheeses = shop.getCheeses();
if (cheeses != null &&
    Array.asList(cheeses).contain(Cheese.STILTON))
    System.out.println("Jolly good, just the thing.");
```
위 코드 대신 다음과 같이 할 수 있다면 좋을 것
```
if (Arrays.asList(shop.getCheeses().contains(Cheese.STILTON)))
    System.out.println("Jolly good, just the thing.");
```

- 하지만 비어있는(길이가 0) 배열이나 컬렉션 대신 null을 반환하는 메소드를 사용할 때는, 어쩔 수 없이 위의 복잡하고 긴 형태(null 여부를 확인하는)로 코드를 작성할 필요가 있음  
- 이런 코드는 에러를 유발하기 쉬움
- 수년동안 모르는 채로 지날 수 있음 

비어있는 배열보다는 null 값을 반환하는 것이 좋다는 주장이 있으나 두가지 면에서 틀림
1. 해당 메소드가 정말로 성능 문제의 원인인지 성능 프로 파일에 나타나있지 않다면, 이런 경우에는 성능을 우려할 것이 못됨
2. 길이가 0인 배열은 불변 객체이고, 불변 객체는 자유로이 공유될 수 있기 때문에, 아무 항목도 반환하지 않는 모든 메소드 호출에서는 똑같은 배열을 반환할 수 있음
  
  
컬렉션으로부터 배열로 항목들을 복사하기 위해 표준 이디엄에서 하는 일
```
private final List<Cheese> cheeseInStock = ...;

private static final Cheese[] EMPTY_CHEESE_ARRAY = new Cheese[0];

public Cheese[] getCheeses() {
    return cheesesInStock.toArray(EMPTY_CHEESE_ARRAY);
}
```

매번 빈 컬렉션을 반환할 필요가 있을 때마다 동일한 불변의 빈 컬렉션을 반환하는 메소드를 만들 수 있음
```
public List<Cheese> getCheeseList() {
    if (cheeseInStock.isEmpty())
        return Collection.emptyList();
    else
        return new ArrayList<Cheese>(cheesesInStock);
}
```

배열 또는 컬렉션 반환 메소드에서 빈 배열이나 컬렉션을 반환하는 대신 null을 반환해야 할 이유가 없음  
null을 반환하는 이디엄은 배열의 길이가 실제 배열과 무관하게 반환되는 C 프로그래밍 언어에서 전달된 것
