# 기계 학습이란?

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/31?category=767742)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Machine Learning이 무엇인지에 대해서 알아보겠습니다.

### 1-1. 머신러닝(Machine Learning)

```
 Arthru Samuel (1959): Machine Learning is a field of study that gives computers the ability to learn without being explicitly programmed
```

Arthru Samuel은 기계학습을 **명시적으로 프로그램이 작성되지 않아도 컴퓨터가 스스로 학습할 수 있는 능력을 제공하는 학문**이라 정의하였습니다.

체커게임을 만들었던 Samuel은 사실 체커게임을 잘 두지 못했지만, 그의 컴퓨터로 하여금 수많은 게임을 플레이하게 하여 어느 위치에 있으면 이기는 경우가 많아지는 지를 분석하고 이기는 방법을 스스로 학습하게 하였으며 마침내 Samuel도 이길 수 없는 수준의 강자를 만들었습니다.

하지만 위의 정의는 너무 모호하고 오래된 것이기에 머신러닝의 대가 톰 미첼(Tom Mitchell)이 정의한 머신러닝(Machine Learning)에 대해서 다시 알아보도록 하겠습니다.

```
Tom Mitchell (1988): A computer program is said to learn from experience E with respect to some task T and some performance measure P,
if its performance on t, as measured by P, improves with experience E
```

머신러닝의 대가 Tom Mitchell은 **컴퓨터가 어떤 작업(T)를 하는데 있어서 경험(E)로부터 학습하여 성능에 대한 측정(P)를 향상시키는 학문**을 기계학습이라고 정의하였습니다.

체커 게임을 예시로 경험(E)은 수많은 체커 게임을 하는 것이고, 작업(T)은 체커 게임을 하는 일이며, 성능 측정(P)은 다음 체커 게임에서 이길 확룔이 됩니다. 앞서 체커게임에서 수많은 게임(T)을 통해서 경험(E)으로부터 승리할 확률(P)을 향상시켰기에 이는 기계학습에 대한 대표적인 예시가 됩니다.

#### 예시 1. 스팸 메일 필터링

예를 들어 우리의 이메일 프로그램이 우리가 스팸으로 지정한 메일들에 대해서 기계학습을 하여 스팸메일을 더 잘 필터링하는 것을 학습한다고 할 때, 여기서 작업(T)는 무엇이 될까요?

바로 이메일들을 스팸인지 아닌지 분류하는 것입니다.

사용자가 스팸인지 아닌지 분류한 이메일들을 검사하는 것은 경험(E)가 되고 올바르게 분류된 메일의 수는 성능 측정(P)가 될 것입니다.

***

### 1-2. 머신러닝 알고리즘(Machine Learning Algorithms)

* 지도 학습(Supervised Learning)
* 비지도 학습(Unsupervised Learning)
* 강화 학습(Reinforcement Learning)
* 추천 시스템(Recommender System)

기계학습에 대한 문제를 해결하는 상황은 크게 2가지로 나누어집니다.

지도 학습(Supervised Learning)은 개발자가 컴퓨터에게 무엇인가를 수행하라고 학습시키는 반면 비지도 학습(Unsupervised Learning)은 컴퓨터가 스스로 학습하게 합니다.

그 외에도 강화 학습(Reinforcement Learning), 추천 시스템(Recommender System) 등이 있는데 이번 포스팅에서는 개요에 대해서만 짚으므로 다음 포스팅에서 2개의 학습 방법에 대해서 자세히 다뤄보겠습니다.
