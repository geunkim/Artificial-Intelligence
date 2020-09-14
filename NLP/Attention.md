# 어텐션(Attention)

## RNN 기반 인코더 - 디코더 

* 인코더
	- 현재의 상태는 현재의 입력과 이전 상태(hidden state)에 의해 결정
	- ![equation](http://latex.codecogs.com/gif.latex?h(t)=f(h(t-1),x(t)))
* 디코더
	- 현재의 상태는 이전 출력과 이전 상태, 컨텍스트 상태에 의해 결정
	- ![equation](http://latex.codecogs.com/gif.latex?s(t)=f(s(t-1),y(t-1), c))






## 어텐선이 필요한 이유

인코더-디코더 모델 중 하나인 seq2seq 모델은 인코더에서 입력 시퀀스를 컨텍스트 벡터라는 하나의 고정된 벡터 표현으로 압축하고 디코더는 이 컨텍스트 벡터를 이용하여 출력 시퀀스를 만들어 내는데 RNN 기반 seq2seq 모델은 다음과 같은 문제가 있다.

* 입력 시퀀스가 매우 길 경우 입력 시퀀스의 모든 정보를 고정된 크기의 벡터 하나로 압축하기 때문에 정보 손실이 발생한다.
* RNN의 문제 문제인 Vanishing Gradient 문제가 존재 한다.

입력 시퀀스가 길어짐에 따라 출력 시퀀스의 정확도가 떨어지는 현상이 발생하는데 이를 보정하기 위해 어텐션 메커니즘이 사용된다. 어텐션 메커니즘은 기존의 방식보다 많은 데이터를 디코더에 전달한다. 


## 어텐션의 기본 아이디어  

디코더에서 출력 단어를 예측하는 매 시점마다 인코더의 전체 입력 문자를 다시 참고하다는 것이다. 
단 입력 문제 전체를 동일한 비율로 참고하는 것이 아니라 해당 시점에서 예측해야할 단어와 연관이 있는 단어 부분을 더욱 집중해서 보게된다.
하나의 컨텍스트 벡터로 인코딩하는 대산 출력의 각 단계별로 컨텍스트 벡터를 생성하는 방법을 학습한다. 


## 어텐션 메커니즘 

재귀 신경망은 과거의 정보를 모두 통합하는 역할을 하나 과거의 내용일수록 점차 망각할 수 있다. 따라서 재귀 신경망으로 인코더를 구현할 경우 입력의 길이가 길어지면 일정한 크기의 벡터로는 입력의 모든 정보를 표현하기 어려워진다. 
재귀 신경망의 은닉층 노드 개수를 증가시키거나 각 과거 시점의 은닉층 상태 정보를 디코더에서 함께 사용하도록 하는 것을 고려할 수 있다.
디코더는 특정 시점의 출력을 결정할 때 인코더의 모든 시점에 대한 은닉층 상태 정보를 필요로 하지 않는다.
예로 한국어 문장을 영어 문장으로 번역하는 경우 한국어 문장의 각 단어는 영어 문장의 모든 단어가 아닌 일부 단어와 대응된다. 그러므로 디코더는 인코더의 모든 시점의 은닉층 상태 모두가 아닌 일부에 주목하여야 한다. 

* 주목 메커니즘: 인코더-디코더 네트워크에서 디코더는 인코더가 만들어내는 정보의 특정 부분에 주목하여 효과적으로 출력을 만들어 내기도 한다. 인코더의 시각적, 공간적 또는 시공간적인 상태들을 결합하여 주목해야 할 부분에 대한 맥락 정보를 만드는 역할을 하는 구성요소 

![image](./attention_mechanism.png)

주목 메커니즘을 사용하는 인코더-디코더 네트워크에서는 인코더가 입력 전체에 대한 하나의 맥락 정보를 만들어 디코더에 전달하는 대신 디코더가 출력을 산출하는 매 시점마다 맥락정보를 계산하여 사용한다. **맥락정보는 해당 시점의 출력을 결정할 때 주목해야하는 입력의 정보와 직전 시점까지의 디코더의 상태를 바탕으로 계산한다.**

다음 그림은 기계 번역과 같이 시퀀스-투-시퀀스 변환을 하는 주목 메커니즘을 포함하고 있는 인코더-디코더 네트워크 구조의 예이다. 
입력 시퀀스 ![equation](http://latex.codecogs.com/gif.latex?x_1,x_2,...,x_N)에 대해서 인코더는 
재귀 신경망(RNN) 또는 양방향 재귀 신경망 등을 사용하여 특정 벡터의 시퀀스 ![equation](http://latex.codecogs.com/gif.latex?h_1,h_2,...,h_N) 를 생성한다.
인코더-디코더 망에서 마지막 시점의 출력 ![equation](http://latex.codecogs.com/gif.latex?h_N) 만이 맥락정보 
![equation](http://latex.codecogs.com/gif.latex?c)로 디코더에 전달된다. 
주목 메커니즘을 사용하면 매 시점 ![equation](http://latex.codecogs.com/gif.latex?n) 별로 해당 시점에 주목해야할 요소를 고려하여 만들어진 맥락정보 ![equation](http://latex.codecogs.com/gif.latex?c_n)가 만들어져 디코더에 전달된다. 

![image](./seq2seq.png)

주목 메커니즘은 인코더의 각 단계별 출력 ![equation](http://latex.codecogs.com/gif.latex?h_i)와 시점 
![equation](http://latex.codecogs.com/gif.latex?n)의 ![equation](http://latex.codecogs.com/gif.latex?h_i)의 중요도를 나타내는 ![equation](http://latex.codecogs.com/gif.latex?\alpha_i^n)를 가중합을 하여 시점 ![equation](http://latex.codecogs.com/gif.latex?n)의 디코더에 대한 맥락 정보 
![equation](http://latex.codecogs.com/gif.latex?c_n)을 계산한다.

![equation](http://latex.codecogs.com/gif.latex?c_n=\sum_{i=1}^N\alpha_i^n\mathbf{h}_i)

앞의 그림의 주목 메커니즘은 시점 ![equation](http://latex.codecogs.com/gif.latex?n)의 인코더 상태인
![equation](http://latex.codecogs.com/gif.latex?h_i)의 중요도 
![equation](http://latex.codecogs.com/gif.latex?\alpha_i^n)을 다층 퍼셉트론(Multi-Layer Perceptron)과 소프트맥스를 사용하여 도출한다. 
다중 퍼셉트론은 소프트맥스를 적용할 값 ![equation](http://latex.codecogs.com/gif.latex?e_i^n) 를 결정한다. 
여기에서 ![equation](http://latex.codecogs.com/gif.latex?e_i^n)는 
시점 ![equation](http://latex.codecogs.com/gif.latex?n-1)의 디코더 상태 
![equation](http://latex.codecogs.com/gif.latex?s_{n-1})과 
![equation](http://latex.codecogs.com/gif.latex?i)번 째 입력 데이터에 대한 인코더의 상태
![equation](http://latex.codecogs.com/gif.latex?h_i)가 서로 부합되는 점수
![equation](http://latex.codecogs.com/gif.latex?score(s_{n-1},h_i))를 나타낸다.
이 점수는 은닉층의 하나인 다층 퍼셉트론의 학습을 통해서 다음과 같이 결정된다.

![equation](http://latex.codecogs.com/gif.latex?e_i^n=\mathbf{v}^T\tanh(W_{\alpha}\mathbf{s}_{n-1}+U_{\alpha}\mathbf{h}_i))

위 식에서 ![equation](http://latex.codecogs.com/gif.latex?v), ![equation](http://latex.codecogs.com/gif.latex?W_{\alpha}), ![equation](http://latex.codecogs.com/gif.latex?U_{\alpha})
는 학습될 가중치이다 

주목 메커니즘에서의 이들 가중치는 인코더-디코더 망이 학습될 때 함께 학습된다. 

![equation](http://latex.codecogs.com/gif.latex?i) 번째 입력 데이터에 대한 인코더 상태
![equation](http://latex.codecogs.com/gif.latex?h_i)의 시점
![equation](http://latex.codecogs.com/gif.latex?n)에서의 중요도
![equation](http://latex.codecogs.com/gif.latex?\alpha_i^n)는 다음과 같이 점수 
![equation](http://latex.codecogs.com/gif.latex?e_i^n)를 사용하여 소프트맥스로 계산한다.

인코더 각 상태의 중요도의 합은 1이 된다.

![equation](http://latex.codecogs.com/gif.latex?e_i^n=\frac{\exp(e_i^n)}{\sum_{k=1}^N\exp(e_k^n))





## Self-Attention






## Graph Attention Network