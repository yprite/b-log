
자바가 안전한 언어이기 때문에 자바를 만족스럽게 사용하게 된 이유



안전한 언어일지라도 우리의 노력없이는 다른클래스들과 독립적인 클래스를 만들기 어려움



우리 클래스의 클라이언트가 불변 규칙을 파괴하기 위해 최선을 다할 거라는 가정하에 방어적으로 프로그램을 작성해야 함


```
Date start = new Date();
Date end = new Date();
Period p = new Period(start, end);
end.setYear(78);	//p의 내부를 변경
```
가변 객체인 매개 변수의 각각의 방어 복사본을 만들어서 생성자에 전달해야 함

```
//수정된 생성자 - 매개변수의 방어 복사본을 만듬
public Period(Date start, Date end) {
	this.start = new Date(start.getTime());
	this.end = new Date(end.getTime());
	
	if (this.start.compareTo(this.end) > 0)
		throw new IllegalArgumentException(start + "after" + end);
}
```
방어복사본은 매개 변수의 유효성 검사에 앞서 만들어야 하며, 유효성 검사는 원본이 아닌 복사본을 대상으로 해야한다는 것에 유의

신뢰할 수 없는 집단에서 서브 클래스를 만들 수 있는 그런 타입의 매개 변수에 대한 방어 복사본을 만들 때는 clone 메소드를 사용하지 않아야한다

Period 인스턴스가 변경될 가능성은 여전히 존재. Period의 접근자 메소드에서 자신의 내부 가변 필드들에 대한 접근을 제공하기 때문

```
//수정된 접근자 메소드
public Date start() {
	return new Date(start.getTime());
}
public Date end() {
	return new Date(end.getTime());
}
```
새로운 생성자와 새로운 접근자 메소드로 교체함으로써 Period는 진정한 불변 클래스가 됨


요약하면, 만일 클라이언트로부터 받거나 또는 반환하는 가변 컴포넌트를 갖는 클래스가 있다면, 그 클래스에서는 그런 컴포넌트를 반드시 방어 복사 해야함
그러나 만일 방어 복사비용이 엄청나게 비싸면, 클라이언트가 그런 컴포넌트를 변경하지 않는다고 클래스에서 신뢰할수 있다면, 방어 복사를 하지 않는 대신 
영향을 받는 컴포넌트를 변경하지 않는 것이 클라이언트의 책임이라는 사실을 문서화해야 함






