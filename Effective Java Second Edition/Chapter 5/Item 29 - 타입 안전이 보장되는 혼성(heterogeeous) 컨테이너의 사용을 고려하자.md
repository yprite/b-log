제네릭은 Set이나 Map과 같은 컬렉셔네, 그리고 ThreadLocal이나 AtomicReference 같은 단일 요소(single-element) 저장 컨테이너에 가장 많이 사용

이 모든 경우에 매개변수화 되는 것이 바로 컨테이너

컨테이너의 특성에 따라 사용 가능한 타입 매개변수의 개수가 자연스럽게 제한


상황에 따라 유연성을 필요로 하는 경우가 있음

컨테이너 대신 키를 매개변수화 하는 것


```
public static void main(String[] args) {
	Favorites f = new Favorites();
	f.putFavorites(String.class, "Java");
	f.putFavorites(Integer.class, 0xcafebabe);
	f.putFavorites(Class.class, Favorites.class);
	String favoriteString = f.getFavortie(String.class);
	int favoriteInteger = f.getFavorite(Integer.class);
	Class<?> favoriteClass = f.getFavorite(Class.class);
	System.out.printf("%s %x %s\n", favoriteString, favoriteInteger, favoriteClass.getName());
}
```

위와 같은 Favorites를 타입 안전 혼성 컨테이너라고 함

Favorites의 구현 코드는 의외로 작음, 아래와 같음

```
public class Favorites {
	private Map<Class<?>, Object> favorites = new HashMap<Class<?>, Object>();
	
	public <T> void putFavorite(Class<T> type, T instance) {
		if (type == null)
			throw new NullPointerException("Type is null");
		favorites.put(type, instance);
	}

	public <T> getFavorite(Class<T> type) {
		return type.cast(favorites.get(type));
	}
}
```

클래스 리터럴 타입은 1.5부터 제네릭화

위 클래스에는 두가지 제약이 있음

첫번째, 클라이언트가 Class 객체를 원천타입의 형태로 사용하면, Favorites 인스턴스의 타입 안전을 쉽게 훼손시킬 수 있다는 것

해결책은 아래와 같음

```
public <T> void putFavorite(Class<T> type, T instance) {
	favorites.put(type, type.cast(instance));
}
```

두번째, 비구체화 타입에 사용될 수 없음

해결책은 있으나 만족스러운 방법은 아님

수퍼타입토큰 기법



```
static Annotation getAnnotation(AnnotatedElement element, String annotationTypeName) {
	Class<?> annotationType = null;
	try {
		annotationType = Class.forName(annotationTypeName);
	} catch (Exception ex) {
		throw new IllegalArgumentException(ex);
	}
	return element.getAnnotation(annotationType.asSubClass(Annotation.class));
}
```

요약하면 컬렉션 API에서 보여주듯이 컨테이너에 제네릭을 사용하면 컨테이너 당 사용가능한 타입 매개변수의 숫자가 데한
그러나 컨테이너 자체보다는 요소의 키에 타입 매개변수를 두면 그런 제약을 극복할 수 있으며, 이 경우 서로 다른 타입의 요소가 저장될 수 있으므로 그런 컨테이너를 혼성 컨테이너라고 함
