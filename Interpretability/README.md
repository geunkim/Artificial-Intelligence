# 해석 가능성(Interpretability)




# Explainable Artificial Interlligence

* 딥러닝의 문제: DNN의 경우 비선형 구조가 중첩되어 모델의 결정 과정의 투명성이 낮음



* 딥러닝의 예측을 설명하기 위한 접근 방법
  - Sensitivity Analysis(SA): 입력 변화에 대한 예측의 민감도 계산
    + 미분을 통해 분류기의 결정의 설명 
  - Layer-wise relevance propagation(LRP) : 입력 변수와 관련하여 결정을 의미있게 분해
  	+ FFNN(feed-forward neural networks), LSTM(long-short term memory), FVC(fisher vector classifiers) 등의 프레임워크 활용 
  	+ 분해를 통해 분류기의 결정을 설명 
    + decompose decision function -> explain subfunctions -> aggregate explainations
  	+ 관련성 보전 (?) 
  	+ 

* Explanation methods
  - Perturbation-Based
  	+ assess features relevance by testing the model to their removal or perturbation
  	+ disadvangates: slow, assumes locality, pertubation may introduce artefacts
  - Function-Based
    + identify the contribution of input features as the first order terms of a Taylor expansion
  - Structure-based
    + LRP: to robustly explain a model, leverage the neural network structure of the decision function

  - Surrogate-/Sampling-Based



## 참고자료 

* 정지훈 교수 동영상 
  - [머신러닝의 해석가능성(Interpretability in Machine Learning](https://youtu.be/hMaB3dMCAzk)
* Dr. Wojciech Samek 
  - [Explainable AI - Methods, Applications, & Recent Developments](https://youtu.be/AFC8yWzypss)
* Keven Clark, Urvashi Khandelwal, Omer Levy, Christopher D. Manning, 
[What Does BERT Look At? An Analysis of BERT's Attention](https://arxiv.org/pdf/1906.04341.pdf)
* Sarthak Jain, Byron C. Wallace, [Attention is not Explanation](https://arxiv.org/pdf/1902.10186.pdf)


* Paper

