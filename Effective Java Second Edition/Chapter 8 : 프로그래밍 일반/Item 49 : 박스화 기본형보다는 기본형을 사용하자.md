
자바는 두 종류의 타입시스템을 갖고 있음
- int, double, boolean과 같은 기본현(primitives)
- String이나 List와 같은 참조 타입(Reference type)

모든 기본형은 자신과 대응되는 박스화 기본형을 갖고 있음
- int <-> Integer
- double <-> Double
- booelan <-> Boolean

자바 1.5 배포판에서 오토박싱(autoboxing)과 오터언박싱(auto-unboxing)이 추가 됨  

기본형과 박스화 기본형 간에는 크게 세 가지 차이점이 존재
1. 기본형은 자신의 값 만을 갖는 반면, 박스화 기본형은 자신의 값과는 별개로 식별성을 갖음 : 두 개의 박스화 기본형 인스턴스가 갖는 값은 같지만 식별성은 다를 수 있다는 의미
2. 기본형은 완전한 기능 값 만은 갖는 반면, 각 박스화 기본형은 자신과 대응되는 기본형이 가질 수 있는 모든 기능 값에 추가하여 비 기능 값인 null을 갖음
3. 기본형은 일반적으로 박스화 기본형에 비해 실행 시간과 메모리 사용 효율이 좋음

```
Comparator<Integer> naturalOrder = new Compartor<Integer>() {
	public int compare(Integer first, Intger second) {
		return first < second ? -1 : (first == second ? 0 : 1);
	}}
```
위 코드는 결함이 존재.  
naturalOrder.compare(new Integer(42), new Integer(42)); 의 결과 값을 호출하면 알 수 있음  
first와 second가 참조하는 Integer 인스턴스들의 값이 오토 언박싱 되면서 자신들의 기본형 값이 추출==비교 연산자를 박스화 기본형에 적용하면 대부분 틀린 결과가 나옴

요약
- 박스화 기본형보다는 기본형을 사용
- 기본형이 더 간단하고 실행 속도가 빠름
- 오토박싱은 박스화 기본형을 사용할 때 코드를 줄여줌
- 두 개의 박스화 기본형을 == 연산자로 비교하면, 값이 아닌 객체 참조를 비교하므로 거의 대부분 false가 됨
- NullPointerException 예외가 발생할 수 있음
- 기본형 값이 오토박싱 될 때는 불필요한 객체가 생성되고 비용도 많이 발생
