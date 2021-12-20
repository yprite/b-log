
 많은 enum들은 본래 단일 int값과 연관됨


잘못된 예
```java
public enum Ensemble {
	SOLO, DUET, TRIO, QUARTET, QUINTET,
	SEXTET, SEPTET, OCTET, NONET, DECTET;

	public int numberOfMusicians() { return ordinal() + 1; }
}
```

이 enum은 잘 동작하지만 유지보수가 문제


상수값의 순서가 바뀌면 메소드에 문제가 생김


해결책은 enum과 연관된 상수 값을 추출할 때 순서를 나타내는 서수를 기준으로 하지 않는 것

그리고 서수는 인스턴스 필드에 따로 저장


```java
public enum Ensemble {
	SOLO(1), DUET(2), TRIO(3), QUARTET(4), QUINTET(5),
	SEXTET(6), SEPTET(7), OCTET(8), DOUBLE_QUARTET(8),
	NONET(9), DECTET(10), TRIPLE_QUARTET(12);

	private final int numberOfMusicians;
	Esemble(int size) { this.numberOfMusicians = size; }
	public int numberOfMusicians() { return numberOfMusicians; }
}
```




