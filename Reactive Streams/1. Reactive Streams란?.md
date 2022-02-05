# Reactive Streams 
## 1. Reactive Streams란?
RxJava 버전이 1.x에서 2.x로 올라간 배경에는 Reactive Streams가 있다.  
Reactive Streams란 라이브러리나 프레임워크에 상관없이 데이터 스트림을 비동기로 다룰 수 있는 공통 메커니즘으로,  
이 메커니즘을 편리하게 사용할 수 있는 인터페이스를 제공

즉, Reactive Streams는 인터페이스만 제공하고 구현은 각 라이브러리와 프레임워크에서 한다.

## 2. Reactive Stream의 구성
Reactive Streams는 데이터를 만들어 통지하는 Publisher(생성자)와 통지된 데이터를 받아 처리하는 Subscriber(소비자)로 구성  
Subscriber가 Publisher를 구독(subscribe)하면 Publisher가 통지한 데이터를 Subscriber가 받을 수 있음  
- Publisher 데이터를 통지하는 생산자
- Subscirber 데이터를 받아 처리하는 소비자

Publisher가 데이터를 통지한 후 Subsriber가 이 데이터를 받을 때 까지의 데이터를 흐름
1. 먼저 Publisher는 통지 준비가 끝나면 이를 Subscirber에 통지(onSubscribe)
2. 해당 통지를 받은 Subscirber는 받고자 하는 데이터 개수를 요청  
(Subscriber가 자신이 통지 받을 데이터 개수를 요청하지 않으면 Publisher는 통지해야 할 데이터 개수 요청을 기다림)
3. Publisher는 데이터를 만들어 Subscriber에 통지(onNext)
4. 이 데이터를 받은 Subscriber는 받은 데이터를 사용해 처리 작업을 수행
5. Publisher는 요청받은 만큼의 데이터를 통지한 뒤 Subscriber로부터 다음 요청이 들어올 때까지 데이터 통지를 중단
6. Publisher는 Subscriber에 모든 데이터를 통지하고 마지막으로 데이터 전송이 완료돼 정상 종료 통지(onComplete)  
(완료 통지를 하고 나면 Publisher는 이 구독 건에 대해 어떤 통지도 하지 않음)
7. Publisher는 처리 도중에 에러가 발생하면 Subscriber에 발생한 에러 객체와 함께 에러를 통지(onError)

[그림 1-5]

Subscriber가 Publisher에 통지 받을 데이터 개수를 요청하는 것은 Publisher가 통지하는 데이터 개수를 제어하기 위함  
[그림 1-6]

Publisher와 Subscriber는 4개 프로토콜과 데이터를 통지  
|프로토콜(Protocol)|설명(Description)
|-|-|
|onSubscriber|데이터 통지가 준비됐음을 통지|
|onNext|데이터 통지|
|onError|에러(이상 종료) 통지|
|onComplete|완료(정상 종료) 통지|

Reactive Streams는 4개의 인터페이스를 제공
|인터페이스(Interface)|설명(Description)
|-|-|
|Publisher|데이터를 생성하고 통지하는 인터페이스|
|Subscriber|통지된 데이터를 전달받아 처리하는 인터페이스|
|Subscription|데이터 개수를 요청하고 구독을 해지하는 인터페이스|
|Processor|Publisher와 Subscriber의 기능이 모두 있는 인터페이스|

## 3. Reactive Streams의 규칙
Reactive Streams는 4개의 인터페이스로 데이터를 통지하는 구조를 제공  
하지만 이 구조가 제대로 동작하려면 Reactive Streams의 규칙을 따라야 한다  
- 규칙 참고 : reactive-streams-jvm/README.md https://github.com/reactive-streams/reactive-streams-jvm/blob/master/README.md  
  
Reactive Streams의 기본 규칙은 다음과 같음
- 구독 시작 통지(onSubscribe)는 해당 구독에서 한 번만 발생
- 통지는 순차적으로 이루어짐
- null을 통지하지 않음
- Publisher의 처리는 완료(onComplete) 또는 에러(onError)를 통지해 종료

추가로 데이터 개수 요청이나 구독 해지를 수행하는 Subscription은 다음과 같은 규칙이 있음
-  데이터 개수 요청에 Long.MAX_VALUE를 설정하면 데이터 개수에 의한 통지 제한이 없어짐
-  Subscription의 메서드는 동기화된 상태로 호출


