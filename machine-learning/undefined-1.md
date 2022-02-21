# 지도학습과 비지도학습

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/31?category=767742)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Supervised Learning(지도 학습)과 Unsupervised Learning(비지도 학습)에 대해서 알아보도록 하겠습니다.

### 1. 지도 학습(Supervised Learning)

#### \[ 지도 학습(Supervised Learning) ]

지도학습에 대한 정의를 먼저 알아보기 전에 지도학습의 예시가 되는 것들에 대해서 익히고 가도록 하겠습니다.

아래와 같은 그림에서 처럼 집의 가격에 대해 예측을 해본다고 가정합시다. 수집한 데이터 집합(Data Set)에 따라 작성한 그래프는 가로 축이 집의 크기이며, 세로축은 집들의 가격이라고 합시다. 이러한 상황에서 어떤 사람이 750 feet 의 집을 판매한다고 가정할 때 얼마를 얻을 수 있는지에 대해 우리에게 물어보았다고 합시다.

우리는 이 문제를 해결하기 위해서 _각각의 값들을 선형으로 근사하게 잇는 알고리즘_을 떠올릴 수 있는데, 데이터집합에 대해 선형 함수를 만들어서 750 feet의 크기라면 대략 150 정도를 얻을 수 있음을 알 수 있습니다. 하지만 선형으로 만드는 알고리즘은 비효율적이기에 2차 함수로 만드는 알고리즘 등을 더 떠올릴 수 있습니다. 이를 이용한다면 약 200정도를 얻을 수 있습니다.

![그림1](https://t1.daumcdn.net/cfile/tistory/994375375A3767BA20)

이러한 것들은 지도학습의 예시가 되는데, 지도학습의 정의가 아래와 같기 때문입니다.

```
특정 입력(Input)에 대하여 올바른 정답(Right Answer)이 있는 데이터 집합이 주어지는 경우의 학습
```

위의 예시에서 각각의 집은 크기(Input)에 대한 가격(Output)이 주어졌고 Supervised Learning은 이러한 입력들을 기반으로 학습하여 새로운 집에 대한 가격을 알아내는 알고리즘을 개발하고 그 가격을 제시합니다. 즉 프로그램은 이러한 정보들을 바탕으로 **Input과 Output에 대한 관계를 유추하여 올바른 해답(Right Answers)을 제시하게 됩니다.**

그리고 지도 학습에는 유추된 알고리즘을 통하여 연속적인 값을 예측하는 회귀분석(Regression)과 어떤 종류의 값인지를 표시하는 분류(Classification)라는 개념이 등장합니다.

\


#### \[ 회귀분석(Regression) ]

Regression은 **Continuous한 연속적인 값을 찾는 것**입니다.

위의 예제에서 처럼 Output은 이산적이고 스칼라 값일 수 있지만 **Input에 대응하는 Output을 분석하여 연속함수를 찾는 과정**이 바로 Regression 입니다. 위의 예제에서 집의 크기(Input)에 해당하는 적절한 집의 가격(Output)을 찾는 것이 Regression의 예시가 되겠습니다.

\


#### \[ 분류(Classification) ]

분류에 대한 예시 역시도 아래의 그림을 참고하여 설명하도록 하겠습니다. 아래의 그래프는 특정한 종양의 크기에 대하여 그 종양이 악성인지 양성인지를 진단하는 그래프입니다. 이때 4\~5 사이의 모호한 종양 크기가 악성인지 양성인지를 구한다고 할 때 결국에 우리가 원하는 결과도 양성이거나 아니거나의 이산적인 값으로 표현이 되는데, 이것이 바로 Classification의 예시입니다.

즉, Classification이란 **Input에 대응하는 Output을 분석하여 Discrete(이산적인) 값을 찾는 것**입니다. 물론 Output이 반드시 0과 1로 표현되는 문제들만이 Classification 문제가 아니고 0, 1, 2, 3, 4 등과 같이 Discrete한 Output을 내는 것 역시도 Classification 문제입니다.

![그림2](https://t1.daumcdn.net/cfile/tistory/99C61B495A37739833)

하지만 단순히 종양의 크기만으로 진단을 내리는 것은 위험하며 같은 크기의 종양이라고 하더라도 나이가 많으면 더 위험할 수 있습니다. 그래서 종양의 크기와 나이 그리고 악성인지를 나타내는 빨간 색의 X와 양성인지를 나타내는 파랑색의 O의 3가지 속성을 이용한 그래프를 활용하여 판단을 내린다고 합시다.

여기서 학습 알고리즘(Learning Algorithm)은 하나의 직선을 그어 양성과 악성을 구분하여 특정 위치의 종양은 양성일 확률이 높음을 판단 할 것입니다. 물론 실제 문제들에서는 2가지 이상의 특징들이 주어질 것이며 **무한한 특징들(Features)을 다룰 수 있다는 것**은 학습 알고리즘의 흥미로운 점입니다.

![그림3](https://t1.daumcdn.net/cfile/tistory/99EBCC355A37773731)

Supervised Learning모델로 Regression과 Classification을 주로 사용하는 알고리즘인 SVM(Support Vector Machine)은 컴퓨터가 무한한 Feature들을 다룸에도 메모리가 부족하지 않게 해주는 깔끔한 수학적인 트릭이 있음을 알려줍니다.

#### SVM(Support Vector Machine) 자세히 알아보기

\[SVM(Support Vector Machine)이란 무엇일까?]\[svm]

***

### 2. 비지도학습(Unsupervised Learning)

#### \[ 비지도학습(Unsupervised Learning) ]

```
특정 입력(Input)에 대하여 올바른 정답(Right Answer)이 없는 데이터 집합이 주어지는 경우의 학습
```

저번의 내용을 통해서 지도학습은 Input에 대해 Right Answer를 가지는 경우의 학습이라는 것을 배웠습니다. 이번에 배울 비지도 학습은 주어지는 데이터들, **Input이 Output에 대한 Right Answer을 가지고 있지 않을 때, Data Set를 Cluster로 분리하는 학습**입니다.

아래의 그림에서는 1개의 데이터 집합이 2개의 클러스터로 구성된다고 판단을 하고 1개의 데이터 집합을 2개의 클러스터로 분리 할 것입니다. 그리고 이것을 비지도 학습 중 하나인 _Clustering Algorithm_이라고 부릅니다. 실제로 구글 뉴스는 수많은 기사들을 보고 분석하여 같은 주제를 가진 기사들을 하나의 클러스터로 만들어 함께 보이게끔 이 알고리즘을 사용하고 있습니다.

즉, **Unsupervised Learning은 Supervised Learning과 다르게 Right Answer이 주어지지 않습니다.** 그러므로 잘못된 Prediction Result에 대해서 Feedback을 받고 교정을 할 수 없습니다. 이러한 알고리즘은 페이스북에서 특정 집단의 사람들을 그룹화하거나, 천문학에서 은하가 어떻게 탄생했는지 분석하기 위해 별들을 모으는데 사용되곤 합니다.

![그림4](https://t1.daumcdn.net/cfile/tistory/99F828455A37C41F1A)

\[svm]: javascript:alert("아직 포스팅하지 않았어요!")

body{ }
