# 언어 모델 (Language Model)

## 언어 모델 이란?

언어 모델은 **주어진 단어들로 부터 다음에 존재할 단어의 확률을 예측하는 모델**이다. 
언어 모델은 직전 n개의 단어 
![equation](http://latex.codecogs.com/gif.latex?w_{t-n},...,w_{t-2},w_{t-1})로 부터 다음에 출현할 단어 
![equation](http://latex.codecogs.com/gif.latex?w_i)를 예측하는 확률 모델이다. 

![equation](http://latex.codecogs.com/gif.latex?P(w_t|w_{t-1},w_{t-2},..,w_{t-n}))

직전 단어의 개수 ![equation](http://latex.codecogs.com/gif.latex?n)은 응용에 따라 결정된다.
![equation](http://latex.codecogs.com/gif.latex?n=1)이면 바이그램(bigram),
![equation](http://latex.codecogs.com/gif.latex?n=2)이면 트라이그램(trigram)이라 하고
일반적으로는 **n-gram** 이라 한다. 



  - 전체 단어 시퀀스 예측

즉, **문장(단어의 시퀀스)의 확률을 예측**하는 모델로 자연어 생성(Natural Language Generation)의 기반이 된다. 
문장의 확률을 예측하기 위해 이전의 단어가 주어졌을 때 다음 단어가 나올 확률을 예측해야 한다. 
언어 모델은 문장 내 단어들의 조합이 얼마나 적절한지, 또는 해당 문장이 얼마나 적합한지 알려주는 일을 한다. 

언어 모델을 만드는 방법에는 크게 통계를 이용한 방법과 인공 신경만을 이용한 방법이 있다. 
딥러닝 기반 자연어 처리 기술인 GPT(Generative Pre-Traning) 또는 BERT가 전부 언어 모델의 개념을 사용하여 만들었다. 

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


### 신경망 모델을 이용한 언어 모델

정해진 개수의 이전 단어들을 입력으로 하고 다음 단어를 출력으로 하는 학습 데이터를 다층 퍼셉트론 또는 딥러닝 신경망으로 학습할 수 있다.
이 때 입력과 출력 단어는 모두 실수 벡터로 표현한다. 
문장은 순차적인 단어들로 구성되기 때문에 다음 단어를 예측할 때 이전 단어들을 순서대로 고려하는 것이 바람직 해서 LSTM 재귀 신경망과 GRU 재귀 신경망을 사용하여 언어 모델을 적용하기도 했다. 

 