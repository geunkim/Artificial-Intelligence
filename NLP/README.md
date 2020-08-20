# NLP(Natural Language Processing) and AI - 자연어와 인공지능

* 텍스트 전처리 (Text Preprocessing): 차연어 처리 용도에 맞게 텍스트를 사전에 처리하는 작업이다.
크롤링 등을 통해 얻어낸 코퍼스(corpus) 데이터를 사용 용도에 맞게 토큰화(Tokenization), 정제(Cleaning), 정규화(Normalization) 등이 필요하다. 

  - 토큰화 (Tokenization): 주어진 코퍼스 데이터에서 토큰(Token)이라 단위로 나누는 작업으로 토큰의 단위는 상황에 따라 다르나 보통 의미 있는 단워로 토큰을 정의힌다. 
  - 어간 추출 (Stemming)과 표제어 추출(Lemmatization)
  - 


- 가짜뉴스 탐지를 위해서 자연어 처리 기능이 요구됨


## 언어 모델 (Language Model)

언어 모델은 **주어진 단어들로 부터 다음에 존재할 단어의 확률을 예측하는 모델**이다.   
즉, **문장(단어의 시퀀스)의 확률을 예측**하는 모델로 자연어 생성(Natural Language Generation)의 기반이 된다. 
문장의 확률을 예측하기 위해 이전의 단어가 주어졌을 때 다음 단어가 나올 확률을 예측해야 한다. 
언어 모델은 문장 내 단어들의 조합이 얼마나 적절한지, 또는 해당 문장이 얼마나 적합한지 알려주는 일을 한다. 

언어 모델을 만드는 방법에는 크게 통계를 이용한 방법과 인공 신경만을 이용한 방법이 있다. 
딥러닝 기반 자연어 처리 기술인 GPT 또는 BERT가 전부 언어 모델의 개념을 사용하여 만들었다. 

* 언어 모델이 필요한 이유?
  - 기계 번역(Machine Translation)
  - 오타 교정(Spell Correction)
  - 음성 인식(Speech Recognition)

* 언어 모델에서 예측하는 확률의 대상은?
  - 문장 전쳬의 확률 예측
  
    ![equation](http://latex.codecogs.com/gif.latex?P(W)=P(w_1,w_2,w_3,w_4,...,w_n)=\Pi_{n=1}^nP(w_i))  
  - 다음 단어 예측: 조건부 확률 적용
   
    ![equation](http://latex.codecogs.com/gif.latex?P(w_n|w_1,w_2,..,w_{n-1}))
  - 전체 단어 시퀀스 예측
  
    ![equation](http://latex.codecogs.com/gif.latex?P(W)=P(w_1,w_2,w_3,w_4,...,w_n)=\Pi_{n=1}^nP(w_n|w_1,w_2,..,w_{n-1}))

   
## 작성...

* ETRI 액소브레인: 언어능력이 높은 인공지능 
* KorBERT(ETRI 국산 언어모델): 학습한 택스트 양이 23Gbyte, 형태소 개수: 47억개 


## 관련 사이트 
* ETRI 인공지능 Open API 서비스
  - 언어분석 API: 행태소 분석, 개체명 인식, 동음이의어/다의어 분석, 의존 구문 분석, 의미역 인식 API
  - 어휘관계 분석 API: 어휘에 대한 정보를 검색하고 어휘들 간의 의미적 연관성을 분석하는 API
  - 질문 분석 API: 사용자의 자연어 질의의 의도를 파악하고 사용자가 요구하는 정답을 찾을 수 있도록 정보를 분석하는 API
  - 음성인식기: 16 kHz Sampling Rate로 녹음된 음성신호에 대해 한국어, 영어, 비원어민이 발성한 영어 음성에 대한 발음 평가 
  
  


## 참고사이트 

* [NLP논문 구현 (Transformer, GPT, EBRT, T5) - Reinforce NLP](https://paul-hyun.github.io/implement-paper/)
* [가짜뉴스를 생성 또는 판별하는 딥러닝 모델 - Grover](http://aidev.co.kr/chatbotdeeplearning/7730)
   - [Defending Against Neural Fake News](https://arxiv.org/pdf/1905.12616.pdf)
* [정민수 - 자연어처리(NLP)](https://medium.com/@omicro03/자연어처리-nip-6일차-언어-모델-8c823466199b)
* [딥러닝을 이용한 자연어 처리 입문](https://wikidocs.net/book/2155)
* [실습으로 배우는 데이터 사이언스](https://programmers.co.kr/learn/courses/21)
* [딥러닝 기반 자연어처리 기법의 최근 연구동향](https://ratsgo.github.io/natural%20language%20processing/2017/08/16/deepNLP/)




