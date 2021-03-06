# 텐서플로우(Tensorflow)

## 생활코딩 야학 : 텐서플로우 (1일차)

텐서플로우를 이용해서 해결하려고 하는 문제는 지도학습의 회귀 문제와 분류 문제이다. 회귀는 숫자로 된 결과를 예측하는 것이고 분류는 범주형 즉, 카테고리 형태의 결과를 예측하는 것이다. 분류와 회귀 문제를 풀기위해서 사용하는 방법은 아주 다양한데 이 방법들을 머신러닝 알고리즘(Machine learning algorithm)이라고 한다. 유명한 것들을 나열해보면 Decision Tree, Random Forest, KNN, SVM, Neural Network 같은 알고리즘이 있다.

이 중 생활코딩 텐서플로우에서 사용 할 알고리즘은 Neural Network이다. Neural Network는 사람의 두뇌가 동작하는 방법을 모방해서 기계가 학습을 할 수 있도록 고안 된 알고리즘이다. 두뇌는 뉴런이라고 하는 세포들이 촘촘하게 연결 되어 있는데 뉴런으로 연결 되어 있는 신경망을 인공적으로 만들었다는 의미에서 인공 신경망이라는 이름을 가지게 되었다.  지금은 Deep learning이라는 이름으로 더 유명하다. 인공 신경망을 깊게 쌓아서 만들었다는 표현으로 딥러닝이라는 단어를 사용하기 시작했고 이 표현이 오늘날 아주 널리 사용되고 있는 것이다. `Neural Network = 인공 신경망 = Deep learning`

사람들은 딥러닝(Deep learning)이 매우 어려운 문제들을 아주 잘 해결할 수 있다는 사실을 발견하면서부터 머신러닝(Machine learning)을 대표하는 용어로 사용하기 시작했고 머신러닝도 인공지능(Aritificial Intelligence)을 대신하는 대표로써 사용되기 시작했다. 하지만 이런 표현들을 엄연히 다른 것이다. 

딥러닝이라는 이론을 공부해서 컴퓨터를 동작시키고 여러가지 문제를 해결하는 것이 쉬운 일이 아니다 불과 몇년전만 해도 아무리 천재라도 대기업이라도 할 수 없는 일이 있었다. 그런 어마어마한 일들이 오늘날에는 딥러닝을 이용하여 해낼 수 있게 되었다. 그뿐만 아니라 구체적인 딥러닝 원리를 몰라도 코드만 작성하면 딥러닝으로 문제를 해결할 수 있는 여러 도구들이 등장 했다. 코딩의 세계에서는 이런 도구들을 라이브러리(Library)라고 부른다. 딥러닝 이론을 코딩으로 이용할 수 있도록 해주는 여러 라이브러리가 있다. TensorFlow, PyTorch, Caffe2, Theano 등이 있다. 

**[라이브러리에서 AI까지 이어지는 계층구조]**

<img width="801" alt="12384" src="https://user-images.githubusercontent.com/54986748/90887265-fd52b900-e3ee-11ea-9f43-370af195e97c.png">

------

​	**[딥러닝 입문]**

1. 파이썬 기초
2. 데이터 입문
3. 머신러닝 이해
4. 딥러닝의 원리
5. 딥러닝 구현

위의 과정은 좋은 방법이지만 상당히 난이도가 높은 과정이다. 그렇기에 이번 야학에서는 원인이 되는 간단한 코드를 작성하고 경험하고 결과로써 코드의 동작과 학습 과정을 구경한다. 그리고 해당 코드를 어떻게 이용하면 좋을지 추측해본다. 원인이 되는 또 다른 형태의 코드를 작성하고 결과를 구경한다. 그렇게 몇가지 코드를 작성하고 결과를 반복하여 구경하면서 딥러닝을 구현하는 시간을 가질 것이다. 그 과정에서 코드와 알고리즘의 동작에 익숙해지는 것이다. 코드로 구현을 하는 수업이다 보니 원리와 수학, 코딩을 완전히 배제할 수 없다는 한계가 있다. 다만 배움을 위해 딱 필요한만큼만 최대한 경제적으로 알려주는 수업이 될 것이라 한다.

------

**지도학습의 과정**

**[머신러닝 프로세스]**

<img width="629" alt="12385" src="https://user-images.githubusercontent.com/54986748/90889726-a0a5cd00-e3f3-11ea-9512-cbcf29b3b7b0.png">

1. 과거의 데이터를 준비합니다.
   1. 과거의 데이터에서 원인(독립변수)과 결과(종속변수)를 의식한다.
2. 모델의 구조를 만든다.
3. 데이터로 모델을 학습(FIT) 합니다.
4. 모델을 이용합니다.

------

**실습 환경 설정**

설치 : 구글 드라이브->새로만들기->더보기->연결할 앱 더보기->Colaboratory 검색 후 설치 

실행 : 구글 드라이브 -> 새로만들기 -> 더보기 -> Google Colaboratory

실습 예제 코드 주소 : https://opentutorials.org/module/4966 (colab 눌러서 공유 가능/colab이 안될 경우 backend.ai 이용)

------

