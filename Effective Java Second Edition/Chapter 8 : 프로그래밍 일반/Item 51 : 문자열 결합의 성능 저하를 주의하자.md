


문자열 결합 연산자를 n개의 문자열에 반복적으로 사용하면 n의 제곱에 비례하는 시간이 소요
이유는 String이 immutable이기 때문이다  
  
```
//문자열 결합의 부적합한 사용 - 말도 안되게 느림
public String statement() {
	String result = "";
	for (int i = 0; i < numItems(); i++)
		result += lineForItem(i); // String 결합
	return result;
}
```
  
원하는 성능을 얻으려면 String대신 StringBuilder를 사용
```
public String statement() {
	StringBuilder b = new StringBuilder(numItems() * LINE_WIDTH);
	for (int i = 0; i < numItems(); i++)
		b.append(lineForItem(i));
	return b.toString();
}
```

### 요약
- 성능을 고려해서 몇개 정도면 몰라도 그 이상의 문자열을 결합할 때는 문자열 결합 연산자를 사용하지 말자
- StringBuilder 클래스와 그 클래스의 append메소드를 사용하자
- 문자 타입을 저장하는 배열을 사용하거나, 문자열을 결합하지 말고 한번에 하나씩 처리하자




