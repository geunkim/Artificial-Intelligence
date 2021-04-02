# Keras 기본 통합 및 즉시 실행 

## 기술적인 요구사항 
- TF 2.0 또는 상위버전 
- 파이썬 3.4+
- Numpy 

## TF 2.0에서 새로운 추상화 

* 추상화: 물리적, 공간적 또는 시간적인 세부 사항을 기술하지 않고 특정 작업이나 작업 셋의 중심이 되는 아이디어를 설명하거나 격리시키는 과정

* 머신러닝(machine learning, 기계 학습) 시스템의 추상화
  - 데이터 학습
  - 모델링
  - 모델 평가
  - 예측
  - 모델 저장 및 로딩 

* Tensorflow의 추상화
  - 데이터 I/O
  - 모델 구축
  - 모델 평가
  - 모델 직렬화 
  - 모델 역직렬화 

## Keras API 
  - 데이터 로딩, 모델 구축, 모델 학습, 모델 평가, 모델 구동, 이전 모델의 로딩과 저장을 위한 API 제공 

## Keras 란?

딥 러닝(Deep Learning) 모델을 학습하고 구축하는데 널리 사용되는 고수준 API

* 모델 학습: 입력 데이터셋에 대해 모델의 파라미터(또는 가중치)를 계산하는 작업
	- Keras에서 모델은 레이어들의 조합을 이용하여 구축
* 추론(inference): 주어진 입력에 대해서 수학적인 코어와 학습된 파라미터를 사용하여 예측 결과를 구하는 과정

### Keras layer API

레이어 API는 정형적인 인터페이스를 유지하고 코드 재사용을 권장하기 위해 객체지향 방식으로 구현 
모든 레이어들은 공통 기능과 특성 셋 및 일 부 동적 별 특성이 있음 

* layer.get_weights(): NumPy 배열의 리스트로 layer의 가중치(weight)를 반환
* layer.set_weights(weights): NumPy 배열의 리스트로 부터 레이어의 가중치를 설정 
* layser.get_config(): layer의 구성이 들어있는 딕셔너리(dictionary)를 반환 

#### tensorflow.keras에 포함된 일반적인 레이어 

* Generic layers

	- dense layer
	- convolutional layer
	- pooling layer
	- recurrent layer
	- activation layer
	- normalization layer

* Common layer
	
	- 입력 레이어(input layer): 사용자로 부터 입력을 받는 placeholder layer 역할을 수행

```Python
layer_name = tf.keras.Input(
	shape=None,
	batch_size=None,
	name=None,
	dtype=None,
	sparse=False,
	tensor=None,
	**kwarges
	)
```

#### 순차형 API를 사용한 모델 

```tf.keras.Sequential```이 기본 구성 요소이며 단순하고 연속적인 구성에 적합 
```add()메소드를 사용하여 구성된 레이어를 결합```

* 모델 구성
	- 네 개의 안전 연결 레이어로 구성된 네트워크 구성 
	- 각 레이어는 10개의 노드 또는 뉴런으로 구성
	- 각 레이어는 ReLU(rectified linear unit) 활성 함수 사용 
	- 최종 출력은 소프토 멕스 레이어 사용 


