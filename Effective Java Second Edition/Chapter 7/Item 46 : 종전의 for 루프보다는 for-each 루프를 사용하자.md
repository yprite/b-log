
자바바 1.5배포판 이전에 컬렉션 요소를 반복 처리하는 이디엄은 다음과 같음

```

for (Iterator i = c.iterator(); i.hasNext()){
	doSomething((Element)i.next());
}

```



배열 요소를 반복 처리하는 이디엄은 다음과 같음

```

for (int i = 0; i < a.length; i++) {
	doSomething(a[i]);
}

```

이 이디엄들은 While 루프보다 더 좋으나 완벽하지는 않음

순환자와 인덱스 변수는 혼라스러우며, 에러가 발생할 가능성이 많음



 for-each 루프에서는 순환자나 인덱스 변수를 완벽하게 감춤으로써 에러 가능성과 혼란을 제거

```

for(Element e : elements) {
	doSomething(e);
}

```

여기서 콜론dms "in(..에 저장된) "으로 읽으면 됨

성능저하 없으며 일부 상황에서는 종전 For 루프에 비해 약간의 성능향상이 있을 수 있음



```

enum Suit {CLUB, DIAMOND, HEART, SPADE}
enum Rank {ACE,DEUCE,THREE,FOUR,FIVE,SIX,SEVEN,EIGHT,NINE,TEN,JACK,QUEEN,KING}

...

Collection<Suit> suits = Arrays.asList(Suit.value());
Collection<Rank> suits = Arrays.asList(Rank.value());

List<Card> deck = new ArrayList<Card>();
for (Iterator<Suit> i = suits.iterator(); i.hasNext(); )
    for (Iterator<Rank> j= ranks.iterator(); j.hasNext(); )
        deck.add(new Card(i.next(), j.next()));
```



위 코드의 문제는 suite 컬렉션의 요소가 고갈되면서 루프에서 NoSuchElementException 예외가 발생



```

for (Iterator<Suit> i = suits.iterator(); i.hasNext(); ) {
Suit suit = i.next();
for(Iterator<Rank> j = ranks.iterator(); j.hasNext(); )
deck.add(new Card(suit, j.next());
}
```
버그가 있는 코드를 고치려면, 외곽 요소를 저장하기 위해 외곽 로프의 유효범위에 변수를 하나 추가해야 함



위의 코드에서 for 대신 중첩된 for-each 루프를 사용하면 문제가 간단히 해결

```

for (Suit suit : suits)
for (Rank rank : ranks)
deck.add(new Card(suit, rank));
```



for-each 루프를 사용할 수 없는 경우가 세가지 존재

1.필터링 - 만일 어떤 컬렉션의 요소들을 오가면서 선택된 요소들을 삭제할 필요가 있다면, 명시적인 순환자를 사용할 필요가 있음

2.변환 - 만일 List나 배열의 요소들을 오가면서 그 요소들의 일부 또는 모든 값을 변경할 필요가 있다면, 요소의 값을 지정하기 위해 List 순환자나 배열의 인덱스가 필요

3.병행 반복처리 - 만일 병행으로 여러 컬렉션의 요소들을 오가면서 처리할 필요가 있다면, 순환자나 인덱스 변수를 명시적으로 제어할 필요가 있음


