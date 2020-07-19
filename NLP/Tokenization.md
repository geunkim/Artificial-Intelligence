# 토큰화(Tockenization)

## 문장과 토큰(Sentence and Token)
문장은 일련의 토큰(token)으로 구성되며 텍스트 토큰은 주관적, 임의적인 성격을 갖는다. 
토큰화는 단어, 문자, n-gram 등의 단위로 이루어 지며, 자연어 처리를 위해서 가장 기본적으로 수행되어야 하는 작업이다.  

### **단어 토큰화** 

문장에서 토큰으로 나누는 작업을 토큰화(Tokenization)라고 하며 상황에 따라 다르며 의미가 있는 단위로 토큰을 정의한다.
단어를 토큰의 기준으로 하는 것을 단어 토큰화라고 한다.
문장에서 토큰을 나누는 기준은 공백(white space), 형태소(morphs), 어절, 비트숫자, 구두점(punctuation) 등 다양하다.
구두점이란 마침표(.), 컴마(,), 물음표(?), 세미콜론(;), 콜론(:), 느낌표(!) 등과 같은 기호이다.
토큰화 작업은 단순히 구두점이나 특수문자를 전부 제거하는 정제(Cleaning) 작업을 수행하는 것 만은 아니다. 구두점이나 특수문자를 
전부 제거하여 토큰의 의미를 잃는 경우가 발생하기도 한다.
영어는 띄어쓰기 단위로 자르면 단어 토큰이 구분이 되는데 한국어의 경우 띄어쓰기로 단어 토큰을 구분하기 어렵다. 

* 단어 토큰화의 예

입력: "Why you need to start strength traning today."

이러한 입력으로 구두점을 제외한 토큰화 작업의 결과는 다음과 같다. 

출력: 'Why', 'you', ;need', 'to', 'start', 'strength', 'traning', 'today'

토큰화 작업은 구두점을 지운 뒤에 띄워쓰기(whitespace)를 기준으로 잘라내는 가장 기초적인 
예제이다. 

### 공개된 토큰 생성 함수(tokenizer)들의 성능 비교 

* **wordPunctTokenizer 함수** 
```wordPuncTokenizer```함수는 NLTK(Natural Language Tool Kit)패키지에서 제공하는 함수로 구두점을 별도로 분류하는 특징을 갖고 있어 ```Don't```를 ```Don```, ```,```, ```t```의 
세 개의 토큰으로 분리되며 ```Jone's```를 ```Jone```, ```'```, ```s```로 다음과 같이 분리한다. 

```python
from nltk.tokenize import WordPunctTokenizer
text = "I can't stop!, Don't be fooled by the dark sounding Mr. Jone's name."
print(WordPunctTokenizer().tokenize(text))
```
``The result of WordPunctTokenizer:`` 

``['I', 'can', "'", 't', 'stop', '!,', 'Don', "'", 't', 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'Mr', '.', 'Jone', "'", 's', 'name', '.']``

* **text_to_word_sequence() 함수**
케라스(keras)에서 제공하는 토큰화 도구로 ```text_to_word_sequence```를 지원한다. 
케라스의 ```text_to_word_sequence```함수는 기본적으로 알파벳을 소문자로 변경하고 마침표, 컴마, 느낌표 등의 구두점을 제거한다. 
``can't``, ``don't``, ``jone's``와 같은 아포스트로피는 보준한다. 

```python
from tensorflow.keras.preprocessing.text import text_to_word_sequence
text = "I can't stop!, Don't be fooled by the dark sounding Mr. Jone's name."
print(WordPunctTokenizer().tokenize(text))
```
``The result of text_to_word_sequence:`` 

``['i', "can't", 'stop', "don't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'mr', "jone's", 'name']``

## 단어장(Vocaburary)
자연어 처리를 위해 고려하는 단어들의 집합으로 단순한 단어의 변형 형태(예: book, books, dog, dogs)도 다른 단어로 인식한다.
텍스트에 서로 다른 단어가 총 1,000개가 존재하면 단어장의 크기는 1,000 이다. 
1,000개의 단어는 인코딩(encoding)과정에서 1번부터 1,000번까지 인덱스를 부여한다. 

컴퓨터는 문자보다는 숫자를 더 잘 처리한다. 그러므로 자연어 처리에서도 문자를 숫자로 바꾸는 기법을 사용하고 있다. 
단어장의 단어들은 중복되지 않는 인덱스(index)를 부여하는 것을 인코딩(Encoding)이라 한다. 
즉 단어들을 컴퓨터가 이해할 수 있는 숫자로 변경하는 인코딩과정이 필요하다. 
  
## 원-핫 인코딩(One Hot Encoding)

단어장을 구성하는 단어의 크기가 ```N``` 개일 때 ```N``` 차원의 벡터를 정의하고 
각 단어를 ```N``` 차원의 벡터에서 표현하고 싶은 단어의 인덱스에 1의 값을 부여하고 다른 인덱스에는 0을 부여하는 
형식으로 관련 단어를 벡터 형식으로 표현하는 것이다. 단어의 인덱스 위치에 있는 값은 1, 나머지는 0으로 구성한다.

  ![equation](http://latex.codecogs.com/gif.latex?x=[0,0,..,0,1,0,..,0.0]\in\{0,1}|V|)
  
* 한계: 단어장의 크기가 커질 수록 벡터의 차수가 지속적으로 증가하게 된다. 
각 단어가 별도의 축을 가지므로 단어의 유사도를 표현하지 못하는 단점이 있다. 
단어간 유사성을 알 수 없다는 점은 검색 시스템 등에서 심각한 문제를 야기한다. 

이러한 단점을 해결하기 위해 단어의 잠재 의미를 반영하여 다차원 공간에 벡터화하는 기법으로 크게 두 가지가 있다. 
첫쨰는 카운트 기반 벡터화 방법으로 LSA, HAL 등이 있으며 둘쨰는 예측기반 벡터화 방법으로 NNLM, RNNLM, Word2Vec, FastText 등이 있다.
카운트 기반과 예측 기반 방법 모두를 사용하는 방법을 GloVe 라는 방법이 있다. 

## 임베딩(Embeding)

각 토큰을 연속 벡터 공간(Continous vector space)에 투영하는 것으로 각 원-핫 인코딩된 벡터(```x```)와
연속 벡터 공간(```W```)을 내적하는 **Table Lookup Up**과정을 거쳐 문장의 토콘은 연속적이이고 높은 차원의
벡터로 변환한다.

* CBoW(Continous bag-of-words)
  - 단어장을 순서가 없는 단어 주머니로 생각하고 문장에 대한 표현을 단어 벡터들을 평균시킨 벡터로 한다.
  - 의미가 비슷한 단어들은 공간 상에서 가깝게 위치하고 의미가 비슷하지 않으면 공간 상에서 멀리 떨어져 있도록 한다. 

* Relation Network(Skip-Bigram)
  - 문장 내의 모든 토큰 쌍에 대해서 신경망을 만들어서 문장 표현을 찾는 것으로 여러 단어로 된 표현을 탐지할 수 있으나 모든 단어 간의 관계를 보기 때문에
  전혀 연관이 없는 단어도 보게 되어 계산 복잡도가 높아진다.
  
* Convolution Neural Network (CNN)
  - **n-gram**을 단어, 다중 단어 표현, 구절, 문장 순으로  


