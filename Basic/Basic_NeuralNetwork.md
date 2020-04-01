# 신경망 이해를 위한 수학 개념 

신경망을 구성하는 수학적인 개념과 신겸망의 작동원리에 대해서 살펴본다. 

## 수학적인 개념 

* 텐서(Tensor): 다차원 배열 형태의 데이터를 위한 컨테이너(container)로 딥러닝의 기본 구성 요소이다. 
텐서는 임의의 차원 개수를 가지는 행렬의 일반화된 모습으로 차원(dimension)을 축(axis)라고도 한다. 축의 개수를 랭크(rank)라고 한다. 

* 텐서 연산 (Tensor Operator)
* 미분 (differential)
* 경사 하강법 (gradient descent)


### 신경망을 위한 데이터 표현 

#### 차원에 따른 자료 텐서 분류

* **스칼라 (0D 텐서)**: 하나의 숫자만 담고 있는 텐서로 ```float32```나 ```float64``` 타입의 숫자가 스칼라 텐서이다. 
스칼라 텐서의 랭크는 0 이다. 

```python
>>> import numpy as np
>>> x = np.array(12)
>>> x                //  array(12)
>>> x.ndim           // 출력은 0
```

* **벡터 (1D 텐서)**: 여러 숫자로 이루어진 배열로 하나의 축만 가진다. 

```python
>>> x = np.array([17, 2, 5, 6, 14, 7])
>>> x                 // array([17, 2, 5, 6, 14, 7])
>>> x.ndim            //  출력은 1

* **행렬 (2D 텐서)**: 벡터의 배열로 2개의 축을 가진다. 첫 번째 축에 놓여 있는 원소는 **행**, 두 번째 축에 있는 원소를
**열** 이라 한다. x의 첫 번쨰 행은 [5, 78, 2,34, 8]이고 첫 번째 열은 [5, 6, 7]이다. 

```python
>>> x = np.array([[5, 78, 2, 34, 0],
                  [6, 79, 3, 35, 1],
                  [7, 80, 4, 36, 2]])
>>> x.ndim             // 출력은 2

* **3D 텐서와 고차원 텐서**: 2D 텐서에 하나 이상의 2D 텐서가 추가되먼 숫자가 채워진 직육면체 형태인 3D 텐서가 된다.

```python
>>> x = np.array([[[5, 78, 2, 34, 0],
                   [6, 79, 3, 35, 1],
                   [7, 80, 4, 36, 2]],
                  [[5, 78, 2, 34, 0],
                   [6, 79, 3, 35, 1],
                   [7, 80, 4, 36, 2]]])
 >>> x.ndim             // 출력은 3

#### 텐서의 3개의 핵심 속성 

* 축 개수(랭크): 자료의 차원을 의미하며 numpy 라이브러리의 **ndim** 속성에 저장된다.
* 크기: 각 축을 따라 몇 개의 원소가 있는지를 나타내는 파이썬의 튜플로 앞의 스칼라 텐서는 ()와 같이 크기가 없다. 
벡터의 크기는 (5,)와 같이 1개의 원소로 이루어진 튜플이고 행렬의 크기는 (3, 5)이고 3D 텐서의 크기는 (2, 3, 5) 이다.
크기는 numpy 라이브러리의 **shape** 속성에 저장된다.
* 데이터 타입: 텐서에 포함된 데이터의 자료형으로 float32, unt8, float64 등이 될 수 있다. 
텐서는 사전에 할당하여 연속된 메모리에 저장되어야 하기 때문에 가변길이의 문자열을 지원하지 않는다. 
(numPy에서 dtype에 저장된다.)

```








## 신경망의 구성 요소 (케라스 관점)

신경망의 핵심 구성요소는 계층(layer)으로 일종의 데이터 처리 필터로 입력 데이터로 부터 유용한 형태의 데이터를 추출하여 출력한다. 
구체적으로 입력한 데이터로 부터 주어진 문제에 대해서 더 의미가 있는 표현 (presentation)을 추출한다. 
딥러닝은 이러한 계층이 여러 개 연결되어 있고 점진적으로 데이터를 정재하는 형태를 구성된다. 
결국 딥러닝 모델은 데이터 정제 필터(계층)이 연속되어 있는 데이터 처리를 위한 여과기와 같다.

```python
from keras import models 
from keras import layers 

network = modes.Sequential()
network.add(layers.Dense(512, activation='relu', input_shape(28 * 28,))
network.add(layers.Dense(10, actiation='softmax'))
```
**Dense**는 완전 연결(full connected) 네트워크를 뜻하는 것이고 **소프트맥스(softamx) 층이 있다. 

* 손실 함수(loss function): 학습과정에 학습 결과와 실제 값과의 차이를 측정하는 방법을 명시한다. 

* 옵티마이저(optimizer): 입력한 데이터와 손실 함수를 기반으로 네트워크를 갱신하는 메커니즘이다.

* 학습과 테스트 과정을 모니터링할 지표(예: 정확도)를 명시해야 한다.  


## 신경망 작동원리 (Keras 관점에서)

1. 학습 데이터 셋 (Traning data set) 과 테스트 데이터 셋 (Test data set) 을 준비하고, 학습 데이터 셋을 네트워크에 입력한다.
2. 신경망은 학습 데이터 셋을 기반으로 학습을 수행하고 모델을 정립힌다. 
3. 테스트 데이터 셋을 활용하여 정립한 모델을 평가한다. 


## 학습 사이트

* [신경망 만들어보고 실습해보기](https://developers.google.com/machine-learning/crash-course/introduction-to-neural-networks/playground-exercises)
* [Forward Propagation](https://colab.research.google.com/drive/1f9_CgOaV0jlJeRnzgim6NNCox4LYY3ue?authuser=2#scrollTo=iuYFBtvQmFeU)
 - 신경망의 Forward Propagation 의 파러미터 설졍 이해 
+ [역전파 알고리즘 이해](https://developers-dot-devsite-v2-prod.appspot.com/machine-learning/crash-course/backprop-scroll)

 



