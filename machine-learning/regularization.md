# Regularization

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/37)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Overfitting(과적합)문제와 이를 해결하기 위한 Regularization(정규화)에 대해서 알아보도록 하겠습니다.

### 1. The Problem of overfitting

#### \[ Example: Linear Regression ]

![그림1](https://t1.daumcdn.net/cfile/tistory/99EAD14A5A53024632)

위와 같은 Linear Regression 집값 예측 문제가 있다고 할 때, 직선의 가설함수를 세울 때, 이차함수의 가설함수를 세울 때, 다차 함수의 가설함수를 세울 때 각각의 상황에 대한 판단이 아래와 같이 내려집니다.

* 직선: Underfitting or high-bias
* 이차함수: Just Right
* 다차함수: Overfitting

직선으로 가설함수를 세우는 경우에는 데이터가 가설함수에 잘 들어맞지 않고 강한 선입견(Pre-Conceptual)을 갖는다고 하여 Underfitting 또는 high-bias 문제를 갖고 있다고 합니다.

2차함수의 가설함수는 size가 커지면 감소하기 때문에 적합한 가설함수는 아니지만 그래도 주어진 데이터들은 꽤나 잘 들어맞는 것으로 보입니다.

다차함수의 가설함수는 지나치게 데이터를 맞추려고 하다보니 커브가 많이 생기고 휘어지는 등 High Variance(높은 분산) 또는 Overfitting(과적합) 문제가 발생합니다. 물론 주어진 훈련용 데이터에 관해서는 매우 좋은 성능을 나타내지만 새로운 Data가 왔을 때 제대로 된 예측을 하기에는 부족합니다.

즉,**많은 Feature를 가지고 있는 경우에 가설함수가 훈련용 데이터에 관해서는 비용함수가 0에 근접할 정도로 매우 잘 맞지만 새로운 데이터들이 오면 일반화를 하는데 실패하는 것**을 과적합 문제라고합니다.

어떤 고차함수를 데이터에 맞추려고 할 때 맞출수는 있지만 **커다란 변동성**을 갖게 되는데, 이러한 변동성에 의해 새로운 examples에 대해서 제대로된 예측을 하지 못하는 문제입니다.

\


#### \[ Example: Logistic Regression ]

![그림2](https://t1.daumcdn.net/cfile/tistory/997798345A530D8D19)

예를 들어 위와 같은 Logistic Regression 문제가 있다고 할 때, 3가지 가설함수 역시도 각각 다른 모습을 보여줍니다.

* 직선: Underfitting or High bias
* 이차식: Just Right
* 다차식: Overfitting or High variance

첫번째 직선의 경우는 직선과 데이터들이 잘 들어맞지 않습니다.

두번째 포물선의 경우에는 우리가 얻을 수 있는 최적의 선으로 보입니다.

마지막으로 엄청 고차원의 가설함수를 만들면 데이터에 딱 맞는 자잘자잘 꼬여진 Decision Boundary를 갖게 되지만 제대로 된 예측을 해내지 못합니다. 이를 Overfitting or High Variance 문제라고 합니다.

\


#### \[ Addressing overfitting ]

그렇다면 먼저 과적합인지를 어떻게 알아낼 수 있을까요?

* 가설함수의 그래프를 그려보기
* 학습데이터가 너무 적지 않은지 검사하기

그리고 이러한 과적합 문제를 해결하기 위해서는 아래의 2가지 방법을 수행하면 됩니다.

* Reduce number of features
* Regularization
* ~~Increase number of training data~~
  * 학습 데이터를 늘리면 과적합 문제를 해결할 수 있지만 일반적으로 어려운 일입니다.

먼저 Feature들 중에서도 중복이 되거나 예측을 하는데 중요한 요소가 아닌 Feature들이 있을 수 있습니다. 이럴 땐 **불필요한 Feature들을 먼저 제거**해주거나 알고리즘이 어떤 Feature을 사용할 것인지 자동으로 선택해주는 _Model Selection Algorithm_ 을 이용할 수 있습니다.

그리고나서 Regularization(정규화)를 해주면 되는데, 정규화는 **모든 Feature들을 유지하되 $θ$의 값을 줄이는 것**으로 $y$를 예측하기 위한 수많은 Feature들이 존재하며 그 Feature들이 y에 영향을 주는 경우에 잘 작동합니다. 즉, Regularization은 모델이 너무 복잡해지지 않도록 임의로 제약을 가하는 것입니다.

***

### 2. Cost Function

#### \[ intuition ]

![그림3](https://t1.daumcdn.net/cfile/tistory/990DAE435A5314AC12)

위와 같은 Linear Regression 집값 예측 문제에서 왼쪽의 경우는 잘들어맞는 경우이며 오른쪽의 경우는 Overfitting이 걸린 경우입니다.

그래서 우리는 $θ\_3$와 $θ\_4$를 최소화하여 $x^3$과 $x^4$의 영향력을 줄이려 합니다. 그렇게 되어 $θ\_3$와 $θ\_4$가 $0$에 근접한다면 가설함수는 2차함수에 근접해는 동시에 더욱 간단하며 smooth해질 뿐 아니라 결과적으로 Overfitting하는 경향이 줄어들 것입니다.

그 방법으로, $θ\_3$와 $θ\_4$에 각각 큰 패널티(Penalty)를 부여하면(여기서는 1000) 학습 알고리즘은 학습 오류를 최소화하는 것보다 $\theta$를 줄이는데 우선 순위를 둘 것입니다.

![그림4](https://t1.daumcdn.net/cfile/tistory/9956CE3F5A3A6F4235)\
🔺참고자료1, 이전에 공부했던 경사 하강법 알고리즘 {: style="text-align:center;"}

따라서 위 방법을 사용하여 $θ$들을 구한 후에 다시 Penalty를 제거함으로써 $θ\_3$와 $θ\_4$를 최소화시킨다면 4차함수 모델을 2차함수의 모델에 거의 근접하도록 만들 수 있습니다.

$$\min_θ[\frac{1}{2m}\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})^2\color{red}{+1000}θ^2_3\color{red}{+1000}θ^2_4]$$

\


#### \[ Regularization ]

* "Simpler" Hypothesis
* Less prone to overfitting

만약 Parameter들이 정규화를 통해 작은 값을 갖게 된다면, 복잡한 커브를 많이 지녔던 가설함수는 더욱 간단해질 것이며, Overfitting의 문제가 줄어드는 경향을 보일 것입니다.

정리하면, 각 $θ$에 패널티를 부여하기 위해서 기존의 비용함수를 아래와 같이 수정할 수 있습니다.

$$J(θ)=\frac{1}{2m}\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})^2 + λ\sum_{j=1}^nθ^2_j$$

여기서 합이 1부터 시작하는 이유는 $x\_0$ 은 1로 고정되어있으므로 줄여줄 필요가 없기 때문입니다. 여기서 $λ$는 Regularization Parameter로 비용함수와 정규화의 균형을 유지함으로 Hypothesis Function을 Simple하게 만들어 Overfitting을 피하게 해줍니다.

![그림5](https://t1.daumcdn.net/cfile/tistory/999A88385A531A3717) {: style="text-align:center;"}

기존에 정규화를 하지 않은 파란색의 함수는 상당히 많이 구부러져 제대로 된 예측을 하지 못하는 반면에 정규화를 하여 보다 smooth하고 simple해진 파란색 함수는 보다 좋은 가설함수로 보입니다.

단, 여기서 $λ$가 너무 크면 Underfitting하는 문제가 발생하여 $θ$들 중에서 $θ\_0$만 남게 될 것입니다. 그러므로 적절한 $λ$ 값을 정해주는 것이 중요합니다.

***

### 3. Regularized Linear Regression

#### \[ Regularized Linear Regression ]

$$J(θ)=\frac{1}{2m}[\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})^2+λ\sum_{j=1}^nθ^2_j]$$

$$\min_θJ(θ)$$

Linear Regression 문제에서 최적의 parameter를 찾는 데에는 Gradient Descent와 Normal Equation을 이용하는 2가지 방법이 있습니다.

\


#### \[ Gradient Descent ]

$θ\_0$는 Penalize 하지 않기 때문에 Regularized Gradient Descent를 위한 알고리즘에서 따로 처리해주어야 합니다.

여기서 일반적으로 $\alpha$는 매우 작은 값이고, $\frac{\lambda}{m}$는 양수며, $m$은 매우 큰 값이기 때문에 $(1 - \alpha\frac{\lambda}{m}<1)$ 즉, $α\frac{λ}{m}>0$ 이므로 이 식은 $θ\_j$가 점점 작아지는 효과를 보여줄 것입니다.

\


#### \[ Normal Equation ]

기존의 $θ=(X^TX)^{−1}X^Ty$ 였다면 Regularized된 Normal Equation은 다음과 같습니다.

$$\theta = (X^TX) + \lambda\begin{bmatrix}0 & 0 & 0 & 0 \\\ 0 & 1 & 0 & 0 \\\ 0 & 0 & 1 & 0 \\\ 0 & 0 & 0 & 1 \end{bmatrix})^{-1}X^Ty$$

여기서 $λ$에 곱해진 행렬은 n개의 Feature들에 $θ\_0$ 가 더해진 n+1, n+1크기의 행렬입니다.

\


#### \[ Non-invertibility ]

예를 들어 $m≤n$ 이라고 할 때, 우리는 $X^TX$ 가 Non-invertible/Singular 라는 것을 알 수 있습니다. 하지만 Regularized Normal Equation을 사용하면 역행렬이 항상 존재하게됩니다.

***

### 4. Regularized Logistic Regression

#### \[ Regularized Logistic Regression ]

![그림6](https://t1.daumcdn.net/cfile/tistory/9994AF505A532D3217)

위와 같은 Logistic Regression 문제를 해결하기 위한 비용함수는 다음과 같습니다.

$$J(θ)=−[\frac{1}{m}\sum_{i=1}^my^{(i)}\log h_θ(x^{(i)})+(1−y^{(i)})\log(1−h_θ(x^{(i)}))]+\frac{λ}{2m}\sum_{j=1}^nθ_j^2$$

#### \[ Gradient Descent ]

Gradient Descent 는 외관상으로 Linear Regression동일한 것으로 보이지만 $h\_θ(x)$ 가 다르기 때문에 다르게 작동합니다.
