# 토큰화(Tockenization)

## 문장과 토큰(Sentence and Token)
문장은 일련의 토큰(token)으로 구성되며 텍스트 토큰은 주관적, 임의적인 성격을 갖는다. 
토큰화는 단어, 문자, n-gram 등의 단위로 이루어 지며, 자연어 처리를 위해서 가장 기본적으로 수행되어야 하는 작업이다.  

## 문장 토큰화(Setence Tokenization)

문장 토큰화는 코퍼스 내에서 문장 단위로 구분하는 작업으로 
문서의 양이 많아 지는 경우 바로 단어 토큰화를 진행하지 않고 문장을 토큰화한 후 1차적으로 정제하고 단어 토큰화를 진행한다.
NLTK에서는 문장 토큰화를 위해 ```sent_tokenize```함수를 지원한다.  

```python
from nltk.tokenize import sent_tokenize

sent1 = "IP 192.168.56.31 서버에 들어가서 로그 파일 저장해서 ukairia777@gmail.com로 결과 좀 보내줘. 그러고나서 점심 먹으러 가자."
sent2 = "Since I'm actively looking for Ph.D. students, I get the same question a dozen times every year."
sent3 = "His barber kept his word. But keeping such a huge secret to himself was driving him crazy. Finally, the barber went up a mountain and almost to the edge of a cliff. He dug a hole in the midst of some reeds. He looked about, to mae sure no one was near."

print("The sentence token of sent1: ")
print(sent_tokenize(sent1))
print("The sentence token of sent2: ")
print(sent_tokenize(sent2))
print("The sentence token of sent3: ")
print(sent_tokenize(sent3))
```
``The sentence token of sent1:``

``['IP 192.168.56.31 서버에 들어가서 로그 파일 저장해서 ukairia777@gmail.com로 결과 좀 보내줘.', '그러고나서 점심 먹으러 가자.']``

``The sentence token of sent2:`` 

``["Since I'm actively looking for Ph.D. students, I get the same question a dozen times every year."]``

``The sentence token of sent3:`` 

``['His barber kept his word.', 'But keeping such a huge secret to himself was driving him crazy.', 'Finally, the barber went up a mountain and almost to the edge of a cliff.', 'He dug a hole in the midst of some reeds.', 'He looked about, to mae sure no one was near.']``


## **단어 토큰화** 

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

## 공개된 토큰 생성 함수(tokenizer)들의 성능 비교 

* **NLTK의 wordPunctTokenizer 함수** 

```wordPuncTokenizer```함수는 NLTK(Natural Language Tool Kit)패키지에서 제공하는 함수로 구두점을 별도로 분류하는 특징을 갖고 있어 ```Don't```를 ```Don```, ```,```, ```t```의 
세 개의 토큰으로 분리되며 ```Jone's```를 ```Jone```, ```'```, ```s```로 다음과 같이 분리한다. 

```python
from nltk.tokenize import WordPunctTokenizer
text = "I can't stop!, Don't be fooled by the dark sounding Mr. Jone's name."
print(WordPunctTokenizer().tokenize(text))
```
``The result of WordPunctTokenizer:`` 

``['I', 'can', "'", 't', 'stop', '!,', 'Don', "'", 't', 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'Mr', '.', 'Jone', "'", 's', 'name', '.']``

* **NLTK의 TreebankWordTokenizer 함수**

```python
from nltk.tag import TreebankWordTokenizer
tokenizer=TreebankWordTokenizer()
text = "I can't stop!, Don't be fooled by the dark sounding Mr. Jone's name. Starting a home-based restaurant may be an ideal."
print(tokenizer.tokenize(text))
```
``The result of TreebankWordTokenizer:``

``['I', 'ca', "n't", 'stop', '!', ',', 'Do', "n't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'Mr.', 'Jone', "'s", 'name.', 'Starting', 'a', 'home-based', 'restaurant', 'may', 'be', 'an', 'ideal', '.']``

* **Keras의 text_to_word_sequence() 함수**

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

## 토큰화에서 고려할 내용 

* **단순하게 구두점 특수 문자를 제외해서는 안된다**

갖고있는 코퍼스에서 단어를 찾아내기 위해, 단순하게 구두점이나 특수 문자를 제외하는 것은 바람직하지 않다. 
마침표(.)의 경우 문장의 경계를 나타내기 때문에 단어를 추출할 때 마침표(.)를 제외하지 않을 수 있다. 

``m.p.h``, ``Ph.D``, ``AT&T``와 같이 구두점을 갖고 있는 단어도 있다. 
화페의 단위와 날짜를 표시하기 위해서 (``$``) 와 슬래시(``/``)를 ``$43.55``, ``07/20/2020``와 같이 사용하기도 힌다.
이 경우 ``43.55``는 43과 55를 분류하지 않고 43.55를 하나로 취급해야 한다.

그리고 숫자 사이에 ``,``가 들어가는 경우도 있다. 

* **줄임말과 단어 내 띄어쓰기가 있는 경우**

토큰화 과정에서 영어의 아포스트로피(')는 압축된 단어를 다시 펼치는 역할을 하기도 한다. 
예를 들어 ``what're``와 ``we're``는 ``what are``와 ``we are``의 줄임말이다. 
앞의 예에서 ``re``는 접어(clicit)라고 한다. 예로 ``I am``을 줄인 ``I'm``이 있을 때 ``m``을 접어라고 한다.

``New York``과 ``rock 'n' roll``의 경우 하나의 단어인데 중간에 띄어쓰기가 존재한다. 
사용 용도에 따라서 하나의 단어 사이에 띄어쓰기가 있는 경우에도 하나의 토큰으로 고려해야 하므로 토큰화 작업 시 하나의 단어로 
인식할 수 있어야 한다. 

* **표준 토큰화 예제**

표준화된 토큰화된 방법 중 하나가 Penn Treebank Tokenization이 있으며 규칙은 다음과 같다. 

* 규칙 1: 하이푼으로 구성된 단어는 하나로 유지한다.
* 규칙 2: ``doesn't``와 같이 아포스트로피로 접어가 함께하는 단어는 분리해 준다. 

앞의 결과를 보면 규칙 1과 규칙 2에 따라 ``home-based``는 하나의 토큰으로 취급하며 ``dosen't``의 경우 ``does``와 ``n't``는 분리된다. 

## 한국어의 토큰화

한국어는 영어와 달리 띄어쓰기로 토큰화하기에 부족하다. 
한국어의 경우 띄어쓰기 단위가 되는 단위를 '어절'이라 한다. 어절 토큰화는 단어 토큰화와 같지 않기 때문이다. 

* **한국어는 교착어**

한국어에는 조사라는 것이 존재한다. 한국어의 경우 '그'라는 단어 하나에 '가', '에게', '와', '를', '는' 등과 같은 다양한 조사가 
글자 뒤에 띄어쓰기 없이 바로 붙게 된다. 한국어 자연어 처리를 할 때 같은 단어여도 다른 조사가 붙어서 다른 단어로 
인식이 되면 자연어 처리가 힘들기 때문에 한국어 자연어 처리에서 조사의 분리가 필요하다. 

즉 띄어쓰기 단위가 영어와 같이 독립적인 단어인 경우 띄어쓰기 단위로 토큰화하면 되나 한국어는 어절이 독립적인 단어로
구성되는 것이 아니라 조사 등이 결합되어 있는 경우가 많아 이를 전부 분리하여야 한다는 것이다. 

* **한국어는 띄어쓰기가 영어보다 잘 지켜지지 않는다**

한국어는 영어와 달리 띄어쓰기가 어렵고 잘 지켜지지 않으나 한국어의 경우 띄어쓰기가 잘 지켜지지 않아도 글을 쉽게 이해할 수 있다. 
반면 영어는 띄어쓰기를 하지 않으면 쉽게 알아보기 어려운 언어이다. 이는 한국어(모아쓰기 방식)와 영어(풀어쓰기 방식)라는 언어적
특성이 원인이 있다. 

## 품사 태깅(Part-of-speech tagging)

* **영문 코퍼스 품사 태깅**

NLTK에서 ```pos_tag```함수를 이용하면 단어 토큰에 품사를 부착하여 투플로 출력한다. 
영어 문장에서 단어 토큰화를 수행한 후 수행 결과에 대해서 품사를 태깅한다.

```python
from nltk.tokenize import TreebankWordTokenizer
from nltk.tag import pos_tag

text1 = "I can't stop!, Don't be fooled by the dark sounding Mr. Jone's name. Starting a home-based restaurant may be an ideal."
text2 = "Emma refused to permit us to obtain the refuse permit"

tokenizer=TreebankWordTokenizer()

words = tokenizer.tokenize(text1);  # text1의 단어 토큰화
pos = pos_tag(words)
print(pos)

words = tokenizer.tokenize(text2)   # text2의 단어 토큰화
pos = pos_tag(words)
print("after TreebankWordTokenizer: ")
print(pos)

tokenizer=WordPunctTokenizer()
words = tokenizer.tokenize(text2)   # text2의 단어 토큰화
pos = pos_tag(words)
print("after WordPunctTokenizer: ")
print(pos)

tokenizer=WordPunctTokenizer()
words = tokenizer.tokenize(text2)   # text2의 단어 토큰화
pos = pos_tag(words)
print("after WordPunctTokenizer: ")
print(pos)

```





* **한국어 코퍼스 품사 태깅** 


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


## References
* [딥 러닝을 이용한 자연어 처리 입문.텍스트 전처리.토큰화](https://wikidocs.net/21698)
* [자연어 처리를 위한 문장 토큰화(Setence tokenization)](https://leo-bb.tistory.com/4)
* [NLP에서의 전처리 방법](https://developer-kelvin.tistory.com/13)



