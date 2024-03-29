# GPT-3
- GPT-3(Generative Pre-trained Transformer 3)는 OpenAI사에서 만든 자연어 처리 모델 / 언어 모델이다. 다르게 표현하면, 딥러닝을 이용해 인간다운 텍스트를 만들어내는 인공지능이다. 이를 통해, 소설, 뉴스 기사 생성 등에 사용 가능하다. (참고로, OpenAI는 일론머스크가 설립했다.)
- GPT라는 모델은 시간에 따라 업그레이드 되면서, GPT-1, GPT-2, GPT-3 순으로 개발되어 왔다. 2019년에 발표된 GPT-2에서도 이미 성능이 너무 뛰어나서, GPT-2가 작성한 글이 마치 사람이 쓴 것 같다는 평가를 받았다. 심지어는 이 때문에 가짜 뉴스로 악용될 소지가 있어 보인다고, 대중에게 공개를 꺼려하기도 했다.
- 2020년에 발표된 GPT-3는 GPT-2에 비해 훨씬 많은 파라미터를 이용(GPT-2: 15억개, GPT-3: 1750억개)해서, 훨씬 더 크고 복잡한 형태의 모델을 만들어 낸 것이다. 그리고 그 결과로 엄청난 성능 향상을 가져왔다.
- GPT-3의 성능을 측정하는 방법으로, GPT-3가 쓴 글을 사람이 쓴 것인지 기계가 쓴 것인지 구분하게 하는 실험을 했는데, 평균적으로 실험 참여자의 48% 정도가 사람이 쓴 것으로 착각했다. 심지어는 어떤 글은 88%가 그 글을 사람이 쓴 것이라고 착각했다.
- OpenAI 에서 GPT-3를 개발한 후, API를 공개 했는데, 세계에 수 많은 개발자들이 그 API를 이용하여 다양한 응용 애플리케이션을 개발 했다.

# 언어 모델, Language Model
그럼 언어 모델이라는게 무엇일까.
언어 모델이란, 문장이(혹은 단어가) 주어졌을 때, 그 다음으로 올 내용으로 자연스러운게 무엇인지 예측하는 것을 말한다.
예를 들면, "오늘 하늘이 매우 맑아서 기분이 ____ " 라는 문장이 주어졌을때, 빈 칸으로 적절한 말은 다음 중에 무엇일까?

1. "좋다"
2. "슬프다"
3. "아직"
4. "나는"
5. "어둡다" 

"좋다"가 가장 자연스럽다.

이것을 응용하면, 어떠한 질문에 답변을 주는 형태로 활용될 수 있을 것이다.
"인류가 전염병에서 벗어나려면 얼마나 걸릴까요?" 라고 질문했다고 해보자.

이 질문에 대답하기 위한,
첫 번째 단어로 "종료일은" 이라는 단어가 자연스럽다. ("종료일은")
그다음 단어로는 "없을" 이라는 단어가 자연스럽다. ("종료일은 없을")
그다음 단어로는 "거라고" 이라는 단어가 자연스럽다. ("종료일은 없을 거라고")
그다음 단어로는 "생각합니다" 이라는 단어가 자연스럽다. ("종료일은 없을 거라고 생각합니다")

이와 같은 방식으로 다음 단어로 적합한 것을 하나씩 물어보면서 반복했을때, 
하나의 완성된 답변이 만들어지는 것이다.

"종료일은 없을 거라고 생각합니다."

# 애플리케이션
이와 같은 방식을 이용하면, 실생활에 다양한 분야에서 이용 가능하다.
OpenAI 에서 GPT-3를 개발한 후, API를 공개 했는데, 세계에 수 많은 개발자들이 그 API를 이용하여 다양한 응용 애플리케이션을 개발 했다. 대표적으로 많은 분들이 떠올릴 수 있는 것 중에는 "번역"이 있겠지만, 그 외에도 다양한 재밌는 것들이 있다.

## React 앱 코딩
예를 들어 자연어로 "Add $3", "Withdraw $5" 버튼을 만들어라, 그리고 Balance를 보여줘라 라고 입력하면,
그에 해당하는 React 코드가 생성되고, 코드 실행 결과도 보여준다.

동작 모습은 아래에서 개발자가 올린 영상을 통해 확인 해보자.
- https://twitter.com/sharifshameem/status/1284095222939451393

## SQL 쿼리 제작
다음과 같이 물어보면서, 내가 원하는 SQL 쿼리도 만들 수 있다. 
"How many users have signed up since the start of 2020?, "What is the average number of influencers each user is subscribed to?"

아래 영상을 통해 알 수 있듯이, 다양한 종류의 문장에 대해서 쿼리문을 생성해내고 있고, 심지어 서브 쿼리까지 만들면서, 섬세하게 동작한다는 것을 알 수 있다.
- https://twitter.com/aquariusacquah/status/1284706786247880705

## 디자인
"내비게이션 바에 카메라, 메세지 아이콘이 있고.. 어쩌고 저쩌고" 작성만 하면 화면이 만들어진다.
- https://twitter.com/jsngr/status/1287026808429383680?ref=gptcrushdemosofopenaisgpt3

## 소설
"I am fine"만 입력해도 그 다음 문장부터는 GPT-3가 다 알아서 만들어준다.
- https://twitter.com/QasimMunye/status/1288912561178640385

## 밈 생성기
사진을 넣으면, 그 사진에 어울리는 밈까지 생성해준다.
사실 개인적으로는 밈이라는 단어자체를 이해한지도 얼마 안됐는데, GPT-3가 일단 나보단 나은 것 같다.
- https://twitter.com/wowitsmrinal/status/1287175391040290816

## 기타 
 재무제표 작성, 이메일 작성, 텍스트 자동 완성, 스펠링 체크, 패러프레이즈 적용 등 수 많은 분야에서 응용되고 있고, 아래 링크를 통해 확인 할 수 있다.
- https://gptcrush.com/

# 기술적으로 무엇이 다른가?
 그럼 기술적으로는 뭐가 그렇게 달라서 GPT-3가 저렇게 대단한 성능을 자랑하는 것일까?
이것을 이해하기 위해서는 자연어 처리 역사를 간단히 파악하면 좋다.

## Word Embedding
 자연어 처리의 첫번째 "사건"이라고 할만한 것은 "Word embedding"의 탄생이었다.
2013년 구글에서 Word embedding이라는 개념을 소개했는데, 말 그대로 단어를 벡터화 시켰다는 것이다.
단어가 벡터의 공간에서 표현되면서, 문맥을 고려할 수 있게 되었다.

![1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FocWXp%2FbtrASBqOrZN%2FUvyObMKeU62BRq0KXUpkf0%2Fimg.png);


간단한 예를 들자면, King, Queen, Princess가 위의 그림과 같이 벡터 공간에 표현이 되어있을 때,
Prince는 어디 있을까? 아마 물음표가 표시되어 있는 위치에 있을거다. 

즉, 단어의 "주변"을 보면 그 단어를 파악할 수 있게 되는 것이다.

다음의 예를 보자. "매나니"라는 단어의 사전적 의미는 이렇다.

![2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcktxjd%2FbtrAVt0W76b%2FpkeGeFKLuOEN1KiO09WODk%2Fimg.png);

그런데 이 단어는 문맥에 따라 서로 다른 의미를 가질 것이다.

그 녀석 무슨 배짱인지 매나니로 와서 일을 하겠다고 한다.
그는 입맛을 잃었다며 매나니로 요기를 하였다.
이런 것들이 벡터 공간에서 다른 벡터들과의 거리와 크기의 영향을 받으면서 문맥적인 의미가 만들어지는 것이다.

## RNN, Seq2Seq
 단어가 어떠한 의미를 가지는 것 까지는 됐지만, 문장을 이해하려면 "순서"를 이해해야 한다.
문장이라는 것은 순서에 따라 다른 의미를 가질 수 있기 때문이다.

예를 들면, "나는 오늘 학교에 가기 싫어요."는 말이 되지만, "가기 오늘 나는 학교에 싫어요."는 말이 안된다.
그래서 나온것이 RNN[1], Seq2Seq[2]이다.

순서를 반영하기 위해서, 모델에다가 단어를 순서대로 집어 넣어서, 문장 벡터에 그 순서까지 반영되게 한 것이다.
예를 들어, "나는 학생 입니다." 라는 문장이 있으면

"나는"
"학생"
"입니다"
를 순서대로 모델에 넣었을때 만들어지는 문장 벡터(정확히는, 문맥 벡터, Context Vector)를 이용해서, 그 문장의 의미를 벡터 공간 내에서 가지도록 하는거다.

만약에 프랑스어를 영어로 바꾸는 번역 Task가 있다고 했을때, 아래의 이미지 처럼, 프랑스어를 벡터 공간에 넣는 과정을 인코딩한다고 하고, 그 인코딩 과정을 통해 만들어진 Context Vector를 이용하여, 영어로 디코딩하는 것이다. 

구글 번역기 같은 것도 간단히 표현하면 이 방식을 응용한거라도 볼 수 있다.
예전에는 문법을 기준으로 문장을 만들어냈다면, 문장을 인코딩하고 디코딩하는 학습 방법을 적용하면서 번역기 성능이 엄청나게 올라갔다.

## 3. Transformer
 그러나 RNN, Seq2Seq 방식의 단점은 문장의 단어를 앞에서 부터 하나씩 순서대로 넣어줘야하기 때문에, 병렬처리가 불가능하고, 따라서 처리 속도가 느리다는 것이다.

또, 입력한 문장이 하나의 고정된 길이의 벡터(Context Vector)로 만들어지게 되는데, 인코딩하려는 문장의 길이가 길어질수록 그 문장을 벡터가 충분히 담지 못하는 문제가 생긴다.

40문장이 넘어가면 표현을 잘 못한다고 알려져 있다.
마치 사람이 통역을 한다고 했을 때, 누군가가 한국말로 여러 문장을 말하고, 그걸 한번에 영어로 통역한다고 한다면,
문장이 길어질수록 모든 문장을 제대로 통역하기 어려워지는 것과 같은 원리이다.

그래서 이러한 문제를 해결하기 위해 나온 것이 Transformer[3]이다.
즉, 문장의 각 속성(단어)을 순서대로 넣지 않고, 고정된 길이의 벡터를 사용하지 않는 방법이다.

순서대로 넣어주는 대신, 문장의 모든 단어를 한번에 입력(벡터 연산) 하되, 순서에 대한 값도 함께 넣어주는 것이다.

나는 학생 입니다
  1      2      3
그리고, 각 단어에 대한 Context Vector를 가질 수 있게 하면서, 문장의 길이가 길어지더라도 정보 손실이 발생하지 않도록 했다.
별 것 아닌 것 같지만, 이 변화가 결국 모델링의 속도(학습 속도)를 엄청나게 빠르게 만들어 주었고(실제로 큰 모델은 모델링 하는 데만 몇 주에서 몇 개월도 걸린다), 문장의 길이에 대한 확장성이 보장되면서 성능이 엄청나게 향상 될 수 있었다.

Transformer에서 또 한가지 중요하게 나오는 개념이 Attention이다.
Attention은 어떤 것에 집중할 것인지를 말하는 것으로, 사람이 문장 번역을 한다고 했을 때도, 매 순간 모든 단어에 동일한 가중치로 집중하면서 해석하지 않는다는 것이다. 그때 그때 집중해야 하는 단어를 보면서 번역한다는 특징을 이용한 것이다.

"나는 학생 입니다"를 영어로 번역한다고 해보자.
"나는"이라는 단어를 번역하기 위해 "I"가 나왔다면, 그 다음에는 "학생"과 "입니다" 중에 "입니다"에 집중(Attention)하여, "am"이라는 번역 결과가 나와야 하고, 그 다음에는 "학생"이라는 단어에 집중하여, "a student"라는 번역 결과가 나오는 것이다.
이렇게 문장 속의 각 단어가 어떤 의미를 가지는지 이해하고, 상황에 따라 특정 부분에 집중하게 하는 방식으로 정확도를 올릴 수 있었다.


# BERT, GPT
구글의 BERT나 OpenAI의 GPT가 Transformer 기법을 활용한 것이다.

구글의 BERT는 OpenAI의 GPT와 성능에서 항상 함께 비교되는 고성능 자연어 처리 모델이다.
참고로 GPT가 처음에 나온게 2017년인데, BERT가 2018년에 GPT가 세운 모든 기록을 다 갈아치워 버린다.
당시에 BERT가 너무 센세이션 해서 TIME지에도 BERT가 표지에 실릴 정도 였다.
그 이후 2019년에 GPT-2를 만들어서 BERT와 거의 유사한 수준의 성능의 모델을 만들어내고,
2020년에 GPT-3를 이용하여 초거대 신경망이라는 것을 만들어서, 그냥 단순히 문장을 디코딩 할 수 있는 수준이 아니라, 다양한 응용이 가능할 정도의 데이터를 집어 넣어 학습 시킨 것이다.
다만 BERT와 GPT는 해결하고자 하는 Task의 특성이 조금 다르다.
BERT의 경우에는 자연어를 해석하여 정량화 하고 분류하는 목적으로 주로 쓰인다면, GPT는 자연어를 해석하여 새로운 문장을 생성하는데 주로 쓰인다.

이런 차이는 BERT와 GPT가 각각 Transformer의 어느 부분을 활용하고 있는지에 따라서 달라진 것이다.
아래에 보이는 이미지가 Transformer의 구조인데, Transformer는 RNN에서 살펴본 것과 같이 Encoder / Decoder 구조를 가지고 있다.

좌측 빨간색 박스로 표현한 부분이 Encoder 부분이며, BERT는 이 Encoder를 활용한 모델이다.
그리고 오른쪽 파란색 박스로 표현한 부분이 Decoder 부분이며, GPT는 이 Decoder를 활용한 모델이다.

![3](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFjz9I%2FbtrAQfJkpVG%2FYvxDvsV5nyZ7ut3SxN8Dy1%2Fimg.png);

인코더는 수 많은 문장을 인코딩하여 벡터 공간에 넣고, 그 수많은 문장들이 공간 속에서 잘 분류된채로 분포시키는 것에 그 목적이 있다고 할 수 있다. 예를 들어, "손흥민이 오늘 골을 넣었다" 라는 문장이 들어왔을 때, 이것이 "스포츠" 내용인지, "정치/경제" 내용인지 구분하게 한다거나, 해당 문장에서 "손흥민"은 사람 이름이고, "골"은 축구 용어라고 구분해 낼 수 있도록 정량화 하고 벡터화 하는 것이다.
(문장을 생성하는 역할은 아니다)

디코더는 이미 세상에 수 많은 문장을 학습 시켜 놓고, 잘 벡터화 되어있는 내용을 토대로, 어떤 샘플이 들어왔을때 그에 해당하는 다른 내용의 단어나 문장을 새로 생성해내는 것에 목적이 있다. 예를 들어, "손흥민이 오늘 골을 넣었다"를 번역하는 Task라면, 벡터 공간에서 해당하는 내용을 찾아 "Heung-Min Son scored a goal tonight."이라고 디코딩한다.

 # 최근 AI 진화 트렌드
최근 초거대 신경망 이라는 단어가 자주 들리는데, 이 단어 자체가 요즘의 인공지능 트렌드를 말해주고 있는 듯 하다.

아래 이미지는 GPT-3가 탄생하기 이전에 빅테크 기업들이 만들어 낸 모델의 파라미터 수를 나타낸 것이다.
GPT-3가 나오기 이전에도 이미 모델의 파라미터 수는 점점 더 많아지는 경향성을 가지고 있었다.

 ![4](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6NV50%2FbtrATcMpqvS%2FCF5uRgysZykxMpZsFIg2S0%2Fimg.png);
 
 이제 아래의 이미지를 보자.
가장 오른쪽 위에 표시된 것이 GPT-3이다. GPT-3가 나타나기 이전의 모델들과는 비교도 안되는 파라미터 수를 가지고 있음을 한 눈에 알 수 있다.

이 빅테크 회사들 입장에선 결국 클라우드를 강조한다. 이런 말이 하고 싶은 거일지도 모르겠다.
"직접 컴퓨터 사서 모델링하려고 하지말고, 그냥 우리껄 써라. 어차피 큰 것이 더 잘된다" 

Open AI도 결국 클라우드 비즈니스이고, 구글도, 마이크로소프트도 자신들의 클라우드를 사용하게끔 유도한다. 

![5](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fz1iL7%2FbtrAZeu0XKP%2FTrAwvSrnPctMvvXzmglhp1%2Fimg.png);

# 초거대 AI들
이처럼 세계 글로벌 기업들이 앞다투어 초거대 신경망을 구축하려고 하고 있다. LG AI연구원에서도 EXAONE이라는 이름의 초거대 신경망을 공개한 바 있다. 기업들이 이런 초거대 신경망 혹은 초거대 AI에 관심을 두는 이유는 이를 통해 다양한 서비스를 개발할 수 있기 때문이다.

앞에서도 말했듯이, 초거대 AI는 그 자체로도 비즈니스 모델이며(OpenAI는 GPT-3를 통해 많은 수익을 창출하고 있다), 글로벌 기업들은 자신들의 기존 서비스와 결합하여 새로운 가치를 제공할 수 있다.

# 한계점
"GPT-3은 너무 과대평가되었습니다. 여러 칭찬은 감사하지만, 여전히 약점이 있고 이상한 실수를 하기도 합니다. AI가 세상을 바꿀 것이지만 GPT-3가 그 첫 발을 내딛은 것뿐이라 생각합니다. 여전히 알아낼 게 많아요." - GPT-3 개발사 대표 Sam Altman

지금까지 내용을 보면 GPT-3 (혹은 그 외 초거대 신경망)은 마치 요술 방망이처럼 보이겠지만, 실상은 그렇지 않다.
"당연히" 여전히 빈틈이 있고, 나아가야 할 방향이 있다.

## 1. 효율성이 너무 떨어진다.
GPT-3은 무려 1,750억개의 매개변수를 가지고 있으며 인간이 평생 보는 정보보다 많은 데이터를 학습해야한다. 사전학습에 필요한 비용, 시간이 너무 방대하고 활용하기도 쉽지 않다.

## 2. 현실 세계의 물리적 상식을 잘 모른다.
GPT-3는 "치즈를 냉장고 안에 넣으면 녹을까?" 라는 질문에 "그렇다"라고 답했는데, 일반적인 사람이 당연히 알만한 물리적 지식을 잘 모른다. 이는 세상을 글로만 학습했기 때문에 눈먼 장님이 방 안에서 책을 통해 세상을 배운 것처럼, 우리가 눈을 통해 현실에서 직접 겪어봐 알 수 있는 매우 당연한 상식을 학습할 기회가 적었기 때문이다. (비전이나 음성 보다 자연어 처리가 특히 어려운 지점이 바로 이 "상식"이다. 사람의 말에는 "상식"이 상당 부분 반영되는데, 기계가 그것을 알기 어려운 경우가 많다)

## 3. 모든 분야에서 뛰어난 것은 아니다.
아직까지는 대부분 태스크에서 사람보다 떨어진 성능을 보이며, 주어진 태스크마다 성능도 매우 차이난다.
예를 들어 두가지 이상의 복합연산 능력이 떨어지고, 태스크를 수행하기 위해 주어진 데이터가 적을수록 성능이 크게 떨어지는 경향을 보였다.

## 4. 학습에 사용된 예제를 외운 것인지 실제 추론한 것인지 구분하기 어렵다.

## 5. 새로운 정보를 수용하기 어렵다. 한마디로 "기억력"이 없다.
현재까지 모든 딥러닝 인공지능이 그러하듯, 학습된 정보를 토대로 입력값에 대해 출력값을 내보낼 수는 있지만, 사람처럼 기억력이라 부를만한 것이 없다. 물론 학습에 사용되는 정보를 입력할 수는 있지만 사람의 기억과는 다를뿐더러 그 크기도 제한되어있다. 또한 새로운 값에 대해 동기화도 잘 이루어지지 않는다.

## 6. GPT-3은 방대한 양의 텍스트를 통해 다음 단어를 예측하는 방식으로 학습되었다.
GPT-3 논문에 서술되어있듯이, GPT-3은 주어진 단어에 대해 통계적으로 가장 어울리는 다음 단어를 생성하는 것 뿐이며 이해하는 것은 아니라는 비판이 있다. 생각과 이해가 무엇인지는 철학의 영역이지만, 분명한건 우리 인간은 다음 단어를 예측하는 방법으로 언어를 학습하지 않았다는 점이다.

# 결론
"AI is the new electrocity." - Andrew Ng

GPT-3는 모델의 크기와 뛰어난 성능으로 많은 관심을 받았다. 또 이것을 이용하여, 기존 모델로는 할 수 없었던, 다양한 작업들이 가능해지면서, 사람들이 상상하던 궁극적인 인공지능 기술에 한 발 다가간 모습이었다. Andrew Ng의 말처럼, 우리가 더 이상 전기 없는 세상에서 살 수 없듯이, 이제는 인공지능 없이 살 수 없는 세상이 만들어질지도 모르겠다.

"Electrocity is the new AI." - Chris Manning

(특히  GPT-3를 기점으로) Open AI, 구글, 엔비디아, 네이버, 카카오, 그리고 LG AI연구원에서도 앞다투어 모델의 크기를 키우고, 학습 데이터를 늘린, 성능이 뛰어난 초거대 언어 모델들을 발표하고 있다. 모델이 커진다는 것은 성능의 향상과 연결된다고 볼 수도 있겠지만, 한편으론 모델의 크기를 키우는데만 연구 자원이 집중되고, 또 인공지능을 활용하고자 하는 다수의 주체가 그런 빅테크 기업에 의존할 수 밖에 없는 구조가 되는 것은 다소 아쉽게 느껴진다. Chris Manning의 말처럼, AI 경쟁이 마치 전기를 누가 더 많이 쓰는지 경쟁하는 것 같다.
