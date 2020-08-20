# 텐서플로우 2.0 기초 

## 요구사항 

* Python 3.4 이상
* 시스템: 우분투 16.04 이상 

## 특성 

* 간결성과 사용 용이
* **tf.keras**와 **즉시 실행(eager execution)**기능을 지원하여 모델 구축이 쉬어짐
* 모든 플랫폼에서 실행될 수 있는 모델 배포 
* 강력한 실험 기법과 연구를 위한 툴
* 직관적인 구성을 위한 단순한 API

* tf.keras
  - 텐서플로우를 쉽게 시작할 수 있도록 해주는 텐서플로우 2.0에서 중심이되는 고수준 API
  - 딥러닝 개념을 독립적으로 구현하는 도구
  - 즉각적인 반복 및 디버깅을 위한 즉시 실행과 같은 기능을 제공

* tf.data
  - 확장성 있는 입력 파이프라인을 구축하는 기능을 제공
  - 많은 양의 데이터를 데이터 메모리에 모두 저장할 필요 없이 디스크로부터 스트리밍할 수 있도록 함

## 텐서플로우 2.0의 새로운 구성 

![텐서플로우 2.0](https://images.app.goo.gl/BXg4BuzCZfnnLsrd6)

인공지능 기술 활용 앱을 개발하는 경우 앞의 다이어그램과 같이 학습(training)과 배포(deployment) 작업이 요구된다. 
텐서플로우는 두 작업을 위한 파이썬 API를 제공한다.
학습 단계는 데이터 파이프라인, 모델 제작, 학습, 그리고 분산 처리 방법들이 포함되며 모델 배포 단계에서는 TF Serving, TF Lite, TF.js와 같은 다양한 배포 방법과 다른 언어에 대한 바인딩 방법을 포함한다.

## 워크플로우

* 학습 데이터 준비
* tf.keras 또는 미리 적성된 추정기(estiator)를 이용하여 모델을 구축, 학습, 검증
* 즉시 실행 기능을 활용하여 모델을 실행하고 디버그하는 단계를 진행 
* 모델을 배포할 준비가 되면, SavedModel 모듈로 모델을 보내 다이어그램에서 보여주는 다양한 방법으로 모델을 배포





* 즉시 실행(eager execution)
 - 그래프들을 그릴 필요 없이 연산을 즉시 실행하는 프로그래밍 환경
 - 모든 연산은 사용자가 나중에 값을 계산할 수 있는 수학적인 그래프를 그리는 대신 실제적인 값을 반환
 - 표준 파이썬 코드 흐름을 따르는 직곽적인 인터페이스를 제공
 
## 텐서플로우 2.0 사용하기

텐서플로우 2.0은 저수준 API와 고수준 API를 이용하는 두 가지 방법 사용이 가능하다.



## 텐서플로우 2.0과 텐서플로우 1.x 비교 

 - TF 1.x에서 ```sess.run``` 으로 실행되던 텐서는 함수가 되었다.
 - feed dict와 placeholder 들이 함수의 인자

## tf.keras

tf.keras는 모델 생성을 위해 다음 3개의 메소드를 제공한다.

 - 순차형(Sequential) API
 	+ TF 1.x에서 모델 생성을 위해 사용한 ```tf.layers``` 모듈이 ```tf.keras.layers```로 변경되었다.
 	+ ```tf.layers```의 많은 메소드가 ```tf.keras.layers```로 복제되었다.
 	+ 순차형 API를 사용하여 모델을 생성하는 것은 심볼릭 ```tf.keras``` 레이어 클래스를 사용하여 선형 모델을 만드는 것으로 완료한다

 ```python
 	model = tf.keras.Sequential([
 		tf.keras.layers.Conv2D(32,2, activation = 'relu',kernel_regularizer = tf.keras.kernel_regularizer.l2(0.04), input_shape=(28, 28, 1)),
 		tf.keras.layers.MaxPooling2D(),
 		tf.keras.layers.Flatten(),
 		tf.keras.layers.Dropout(0.1),
 		tf.keras.layers.Dense(64, activation='relu'),
 		tf.keras.layers.BatchNormalization(),
 		tf.keras.layers.Dense(20, activation='softmax')
 		])
 ```  

 - 함수형(Functional) API

 이전 레이어의 출력 텐서에서 레이어 클래스들을 호출하는 것을 기반하기 때문에 순차형 API보다 더 유연성이 높다. 
 Inception 및 ResNet 아키텍저와 같은 비선형 모델 및 아키텍처를 구현할 수 있다.

 - 모델 서브클래싱(subclassing) 기술

텐서플로우에 포함되지 않은 기술과 기법으로 구현된 커스텀 모델과 레이어를 만드는데 이용한다는 점에서 저수준의 접근 방식이 매우 유용하다.
```tf.keras.Model``` 기반 클래스로 부터 상속되는 클래스를 생성하는 것과 관련되며 입력 인수와 학습 인수를 취하도록 호출 메소드를 정의한 다음 
모델로 부터 전방향 패스의 결과를 계산하고 반한한다.



