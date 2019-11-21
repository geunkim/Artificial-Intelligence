# 개발 환경 구성 


## 아나콘다 

* Anaconda(아나콘다): 가장 인기있는 파이썬/R 데이터 사이언스 플랫폼

  * 단일 머신에서 개발, 테스트, 교육을 위한 산업 표준으로 Linux, Windows, MacOS X 에서 동작 (Industry standard for developing, testing, and traning on a single machine)
  * **Conda**로 라이브러리, 종속성, 환경 관리 (Manage libraries, dependencies, and environments with Conda)
  * 머신러닝과 딥러닝 모델 개발 및 학습 (Develop and train machine learning and deep learning model with ...)
  * 확장성과 성능을 갖는 데이터 분석 (Analyze data with scability and performance with ...)
  * 결과의 시각화 (Visualize results with ...)
  
  * 장점: 환경 파일을 통해 손쉽계 개발환경을 서로 공유
  
* [아나콘다 배포 사이트: Anaconda 2019.10 for macOS Installer](https://www.anaconda.com/distribution/)
* 아나콘다는 실습을 위한 별도의 파이썬 가상환경을 제공
  
### 자동 환경 구성

MacOS X 사용자는 다음 명령을 싱행한다.

```shell
~$conda env create -f wikiml_mac.yml
```
실습에 필요한 모든 파이썬 라이브러리가 자동으로 설치한다. 
아나콘다는 실습을 위한 별토의 파이썬 가상환경을 제공하고 있어 실습이 필요할 때 아래의 명령어를 먼저 실행한다.

```shell
~$conda activate wikiml
```
앞의 명령어를 실행하면 아래와 같이(wikiml)이라는 가상환경이 적용된 것을 확인할 수 있다.

```shell
(wikiml)$
```

다음 명령을 입력해서 주피터 노트북을 실행할 수 있다.

```shell
(wikiml)$jupyter notebook
```

실습을 마무리하고 실습용 가상환경을 종료하기 위해서는 다음 명령어를 입력한다.

```shell
~$conda deactivate
```

### 주피터 노트북 (Jupytier Notebook)
주피터 노트북은 브라우저에서 작동하는 파이썬 코드 작성 도구로 코드의 가독성이 높고, 데이터 시각화가 용이하며, 필요한 코드 부분만 따로 실행할 수 있어 코드 작성과 디버깅이
수월하다. 주피터 노트북의 설치 명령어는 다음과 같다.

```shell
~$conda install jupyter notebool
```


  
 
  
