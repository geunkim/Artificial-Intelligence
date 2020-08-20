# BERT(Bidirectional Encoder Representaitons from Transfomers)

## 개요

BERT는 2018년 11월 구글의 Jacob Devlin과 동료가 만들어 공개한 트랜스포머 기반 언어 모델로 새로운 
Language Representation Model이다.  
BERT는 언어표현 사전학습의 새로운 방법으로 위키피디아와 같은 대량의 텍스트 코퍼스(corpus)를 이용한 비지도 학습(unsupervised learning) 방식을 택하였고 범용 목적의 언어 이해(language understanding) 모델을 혼련시키는 것을 목적으로 하는 **사전 훈련 언어모델**이다. 

자연어 처리를 위한 임베딩 방식으로 BERT등장 이전의 Word2Vec, GloVe, Fasttext 방식을 많이 사용하였다. 

텍스트 분류모델을 구성하기 위해 BERT를 사용하는 경우와 사용하지 않은 모델링 두 가지 방법을 고려할 수 있다.

* BERT를 사용하지 않는 일반 모델링 과정
  - 분류를 원하는 데이터를 기반으로 LSTM, CNN 등의 머신러닝 모델을 활용하여 분류

* BERT를 사용한 모델링 과정
  - 대량 텍스트 코퍼스를 기반으로 BERT 언어 모델을 반영하고, BERT 언어 모델의 출력을 추가적인 머신러닝 모델을 쌓아 원하는 작업을 수행 

## BERT 내부 동작 과정 

### BERT 입력 표현(Input Representation)

![BERT](https://blog.kakaocdn.net/dn/bABsUL/btqzmTU7OLm/YwK6JLhNfTYvxkiFzkfkCK/img.png)

<출처: >

 BERT 입력 표현: 입력 임베딩은 토큰 임베딩(Token embedding), 세그먼트 임베딩(Segment embedding), 포지션 임베딩(Position embedding)으로 구성된다.

* 토큰 임베딩 

사용하는 임베딩 방식은 Word Piece 임베딩 방식으로 자주 등장하면서 가장 긴 길이의 서브 워드(subword)를 하나의 단위로 구성한다. 자주 등장하는 서브 워드는 그 자체가 단위가 되고 자주 등장하지 않는 단어는 다시 서브 워드로 분해된다. 기존 워드 임베딩 방식은 Out-of-Vocabulary(OOV) 문제가 있었다. 즉 희기 단어, 이름, 숫자나 단어장에 없는 단어의 학습, 번역에 어려움이 있다. 
Word Piece 임베딩은 모든 언어에 적용가능하며 서브 워드 단위로 단어를 분리하기 때문에 OOV 처리에
효과적이고 정확도를 높인다. 

* 세그먼트 임베딩

문장 임베딩 - 토큰화된 단어들을 하나의 문장으로 만드는 작업으로 BERT에서는 두 개의 문장을 구분자를 넣어 구분하고 두 문장을 하나의 세그먼트로 지정하여 입력한다.
BERT에서는 입력 길이가 제횐되어 있으며 한 세그먼트의 크기는 512개의 서브 워드 이하로 제한한다.
한국어의 경우 보통 20 서브 워드가 한 문장을 이루며 대부분의 문장은 60 서브 워드를 넘지 않기 떄문에 두 문장이 합쳐진 하나의 세그먼트를 128개의 서브 워드로 제한하여도 충분하다. 
긴 문장이 있으면 먼저 입력 길이를 128로 제한하여 학습한 후 128보다 긴 입력을 모아 추가 학습하는 방법을 적용한다. 

* 포지션 임베딩 

BERT 저자는 CNN, RNN과 같은 모델 대신 Self-Attention 모델을 사용하는 모델인 Transformer모델을 발표하였다.
Self-attention은 입력의 위치를 고려하지 않고 입력 토큰의 위치 정보를 고려한다. 
Transformer 에서 Sinusoid 함수를 이용하여 포지션 인코딩을 하는데 BERT에서는 이를 변형하여 포지션 인코딩을 사용한다. 
포지션 인코딩은 단순히 토큰 순서대로 0, 1, 2, .. 와 같이 순서대로 인코딩한다. 


BERT는 총 33억 단어[BookCorpus(8억 단어), Wikipedia Data(25억 단어)]의 거대한 코퍼스를 정제하고 임베딩하여 학습시킨 모델이며 스스로 라벨을 만들고 수행하므로 준지도(Semi-supervised) 학습을 수행하였다. 

BERT는 Transformer를 기반한다. Transformer 모델 구조는 인코더-디코더 모델로 번역 도메인에서 최고 성능을 보였다. Transformer는 CNN, RNN을 이용하지 않고 Self-attention 이라는 개념을 도입하였으며 BERT는 Transformer의 인코더-디코더 중 인코더만 사용하는 모델이다. 

BERT는 BERT-base(L=12, H=768, A=12), BERT-large(L=24, H=1024, A=16)의 두 가지 버전이 있다. 
여기서 L은 Transformer 블록의 숫자이고 H는 hidden size, A는 Transformer의 attention block의 수이다. 
BERT-base는 1.1억 개의 학습 파라미터, BERT-large는 3.4억 개의 학습 파라미터가 존재한다. 

* 임베딩 취합

BERT는 앞에서 설명한 3가지 입력 임베딩을 취합하여 하나의 임베딩 값으로 만든다. 이 합에 Layer normalization과 Dropoup을 적용하여 
입력으로 사전 학습 기능 블록에서 사용한다. 


BERT를 이용한 자연어 처리는 인코더가 입력 문장들을 임베딩하여 언어를 모델링하는 **언어 모델링 과정**과 이를 **상세 튜닝**하여 여러 자연어 처리 타스크를 수행하는 과정으로 이루어진다. 


### Pre-Training(사전 학습)

데이터를 임베딩하여 훈련시킬 데이터를 모두 인코딩이 끝났으면 사전 훈련을 수행한다. 

* 기존의 사전 학습 방법
  - 보통 문장을 왼쪽에서 오른쪽(left-to-right)으로 학습하거나 오른쪽에서 왼쪽(right-to-left)으로 학습하여 다음 단어를 예측하는 방식
  - 예측할 단어의 좌우 문맥을 고려하여 예측하는 방식

* BERT의 사전 학습 방법

  - MLM(Masked Language Model)
  	+ 입력 문장에서 임의로 토큰을 가리고(Mask), 그 토큰을 맞추는 방식의 학습
    + 문장의 빈칸 채우기 문제를 학습
    + 서브 워드 단위로 쪼개진 토큰을 가리는 것이 아니라 한 단어를 통째로 가리는 whole word masking 방법을 사용하기도 하며, 한국어는 서브 워드 단위로 나누는 것 보다 형태소 단위로 나누어 마스킹하는 방식이 더 효과가 좋다고 알려져 있음 
  - NSP(Next Setence Prediction)
  	+ 두 문장이 주어졌을 때 두 문장의 순서를 예측하는 방식으로 두 문장 간 관련이 고려되어야 하는 NLI(Natural Language Inference)와 QA(Question Answering)의 미세 조정(fine tunning)을 위해 두 문장의 연관을 맞추는 학습을 진행

### Transfer Learning(전이 학습)

학습된 언어 모델을 전이학습시켜 실제 자연어 처리 타스크를 수행하는 과정이다. 
전이 학습은 라벨이 주어지는 지도(Supervised)학습 방법을 택한다. 
전이 학습은 BERT 언어 모델에 NLP 타스크를 위한 추가적인 모델을 쌓는 것이다. 
전이 학습을 통해 해결하는 대표적인 문제는 다음과 같이 개체명 분석과 질의 응답 문제가 있다. 

* 개체명 분석(NER: Named Entity Recognition) 문제
  - 문장을 구성하고 있는 요소 중 특별하게 취급하고자 하는 개체에게 속성(entity)을 부여하고 그 것을 관리하는 문제 
  - 날짜, 사람이름, 시간, 기관명 등을 개채명으로 정의하여 문장을 분석하는 기술

* 질의 응답(QA: Question Answering) 문제
  - 자연어로 이루어진 질문에 자동으로 응답하는 시스템 관련 문제  


## BERT 응용 


















#### KorQuAD: 구글의 SQuAD와 같은 데이터를 LG CNS가 한국어로 만든 데이터 셋















언어 모델: 주어진 단어들로 부터 다음에 존재할 단어의 확률을 예측하는 모델

## References

* [BERT에 대해 쉽게 알아보기1 - BERT는 무엇인가, 동작구조](https://ebbnflow.tistory.com/151)
* [BERT 톺아보기](http://docs.likejazz.com/bert/)
