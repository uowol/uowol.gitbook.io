# Logistic Regression

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/36)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Classification(분류)문제 해결을 위한 Logistic Regression에 대해서 알아보도록 하겠습니다.

### 1. Classification

#### \[ Classification ]

우리가 앞에서 배운 Linear Regression이 주어진 Feature에 대해 Continuous(연속적인)한 Value를 Predict하는 방법이였다면, Classification은 **주어진 Feature에 대해 Data들을 Discrete(이산적인)한 Class로 분류하는 방법**으로 우리가 예측하기를 원하는 값 y는 분류된 클래스들 중 하나의 영역에 속하게 됩니다.

Classification문제의 예시로는 아래와 같은 것들이 있습니다.

* Email: Spam or Not Spam?
* Online Transactions: Fraudulent(Yes / No)?
* Tumor: Malignant / Benign?

예측값 y가 0이면 Negative Class 그리고 y가 1이면 Positive Class가 됩니다. 물론 Negative 와 Positive의 경계가 애매모호하기도 하고, 실제로는 분류되는 Class가 여러 개로 나누어지는 Multi-class Classification 문제인 경우가 많지만 우리는 0 or 1로 나누어지는 Binary Classification 문제를 먼저 다루어보도록 하겠습니다.

![그림1](https://t1.daumcdn.net/cfile/tistory/9961FC345A4CAA9F0A)

\


#### \[ Classification for Linear Regression ]

예를 들어 아래의 그림과 같이 Tumor가 Malignant한지 아닌지를 판단하는 Classification 문제가 있다고 할 때, 아직 Classification 문제를 해결하는 방법을 배우지 못한 우리가 할 수 있는 것은 앞에서 배운 Linear Regression을 적용하여 Data에 맞는 직선을 구하는 것입니다.

아래의 왼쪽 그림과 같은 Training Set에서 $h\_θ(x)=θ^Tx$ 를 구하면 파랑색의 직선이 나오고 우리는 예측값이 0.5보다 크면 Malignant라고 예측할 수 있습니다. 그리고 이것은 꽤나 잘 들어맞는 것처럼 보입니다.

* If $h\_θ(x)≥0.5$, predict "$y=1$"
* If $h\_θ(x)<0.5$, predict "$y=0$"

![그림2](https://t1.daumcdn.net/cfile/tistory/99817D4A5A4CAD392C)

하지만 만약 오른쪽의 그림처럼 새로운 Example이 추가되었다고 할 때, y=0.5 의 기준점인 Tumor Size가 오른쪽으로 치우치면서 직선은 더 눕히게 되고 잘못된 예측을 하게 됩니다. 또한 Linear Regression을 적용하면 $h\_θ(x)>1$ or $h\_θ(x)<0$ 인 경우도 발생합니다.

그래서 우리는 **Classification을 위한 알고리즘으로 $0 \leq h\_\theta(x) \leq 1$ 을 만족**하는 Logistic Regression에 대해 배우도록 하겠습니다.

\*\* 이름은 Logistic Regression이지만 Classfication을 위한 알고리즘이므로 헷갈리시면 안됩니다\*\*

***

### 2. Hypothesis Representation

#### \[ Hypothesis Representation ]

이번에 알아볼 Hypothesis Representation은 우리의 가설을 표현하기 위한 함수입니다. $ 0 \leq h\_\theta(x) \leq 1 $ 을 원하는 상황에서 우리가 위에서 세운 가설함수 $h\_θ(x)=θ^Tx$ 는 범위를 만족하지 않으며 잘못된 예측을 할 수 있어서 적합하지 않습니다.

때문에 Logistic Regression 에서는 $h\_θ(x)=g(θ^Tx)$ 로 가설함수를 표현합니다. 그리고 여기서 $g(z)=\frac{1}{1+e^{−z\}}$ 이므로 이를 정리하여 나타내면 아래와 같습니다.

$$h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx}}$$

이 그래프는 0과 1로 수렴하며 그래프의 개형은 아래와 같습니다.

![그림3](https://t1.daumcdn.net/cfile/tistory/99F89C335A4CE10F1A) {: style="text-align:center;"}

덧붙여서 여기에 자연상수 e 대신 다른 수를 집어 넣으면 형태는 비슷하나 기울기가 다른 곡선이 만들어집니다.

Your browser does not support the video tag.

이제 우리가 해야 할 것은 파라미터 $θ$ 들을 데이터에 맞추는 것입니다. 우리는 주어진 Training Example로부터 $θ$를 정하고 이 가설함수를 통해 예측을 할 수 있습니다.

하지만 $θ$ 를 구하는 알고리즘을 배우기 전에 $h\_θ(x)$ 에 대해 해석해보도록 하겠습니다.

\


#### \[ Interpretation of Hypothesis Output ]

$$h_θ(x)=P(y=1|x;θ)$$

h의 출력값은 Feature X를 가지고 있는 경우에 $y=1$인 Class에 들어갈 확률을 의미합니다. 예를 들어 입력벡터 x가 아래와 같다고 할 때 $h\_θ(x) = 0.7$ 이라는 것은 Tumor가 Malignant일 확률이 70%라는 것을 의미합니다.

또한 결국에 입력 x의 결과는 Class1 또는 Class0에 속해야 하므로 $y=1$ (Class1)일 확률과 $y=2$ (Class2)일 확률의 합은 1이 되어야 합니다.

$$P(y=0|x;θ)+P(y=1|x;θ)=1$$

![그림4](https://t1.daumcdn.net/cfile/tistory/9902773F5A4D7AFF14) {: style="text-align:center;"}

***

### 3. Decision Boundary

#### \[ Logistic Regression ]

이번에 우리가 공부할 내용은 언제 이 가설이 $y=1$임을 예측하고 언제 $y=0$임을 예측하는가(어떠한 경계를 기준으로) 그리고 1개 이상의 Feature를 가질 때 어떤 모습을 보이는가 입니다.

앞서서 우리는 $h\_θ(x)=g(θ^Tx)$ 이며 $g(z)=\frac{1}{1+e^{−z\}}$ 임을 배웠고, 아래와 같이 판단한다고 이야기했습니다.

* If $h\_θ(x)≥0.5$, predict "$y=1$"
* If $h\_θ(x)<0.5$, predict "$y=0$"

위의 그래프의 개형은 아래와 같으며 $h\_θ(x)≥0.5$ 인 부분은 $z≥0$ 인 영역과 같습니다. 그렇다면 $y=0$인 Class0에 속하는 경우는 언제일까요? 바로 $z<0$ 인 영역이며 $z=0$을 기준으로 Class가 나뉘어지고 있으므로 Decision Boundary는 $z=0$이 됩니다.

![그림3](https://t1.daumcdn.net/cfile/tistory/99F89C335A4CE10F1A) {: style="text-align:center;"}\


#### \[ Decision Boundary ]

$x1$,$x2$ 를 Feature로 갖는 Training Set이 아래와 같이 주어졌다고 하고, 가설함수는 $h\_θ(x)=g(θ\_0+θ\_1x\_1+θ\_2x\_2)$ 라고 할 때, 아직 $θ$ 를 구하는 방법은 배우지 못했으므로 각각의 $θ$ 를 $-3$, $1$, $1$ 이라고 가정하겠습니다. 이때 $h$는 언제 $y=1$ 또는 $y=0$으로 예측을 할까요?

![그림5](https://t1.daumcdn.net/cfile/tistory/990D78385A4D863603) {: style="text-align:center;"}

우리는 위에서 배운 내용들로 $θ^Tx=z$ 에 해당하는 $−3+x\_1+x\_2≥0$ 이라면 $y=1$로 예측할 것임을 알 수 있고, 이 영역은 위의 초록색 영역으로 나뉘어진 영역들 중 1시 방향의 영역을 의미합니다.

반대로 $z=−3+x\_1+x\_2<0$인 부분은 7시 방향의 영역으로 $y=0$인 Class에 속하게 되고, 여기서 생긴 경계(직선)이 Decision Boundary가 됩니다.

정리하자면 **Decision Boundary는 Class들을 나누는 경계**를 의미합니다. 그리고 이러한 Decision Boudary는 Training Set이 아니라 Property로 $θ$ 벡터에 의해 결정이 됩니다.

\


#### \[ Non-Linear Decision Boundaries ]

이번에는 보다 복잡한 예시의 Decision Boundary에 대해 알아보도록 하겠습니다.

예를 들어 아래의 그림과 같은 Data Set이 주어졌다고 할 때, 직선으로 Class를 구분하는 것은 불가능해보입니다. 가설함수를 $h\_θ(x)=g(θ\_0+θ\_1x\_1+θ\_2x\_2+θ\_3x^2\_1+θ\_4x^2\_2)$ 와 같이 세웠다고 할 때, 5개의 Parameter들이 순차적으로 $-1$, $0$, $0$, $1$, $1$ 을 갖게 된다고 합시다. 그렇다면 우리는 아래와 같이 예측을 할 수 있습니다.

* Predict "$ y=1 $" If $−1+x^2\_1+x^2\_2≥0$
* Predict "$ y=0 $" If $−1+x^2\_1+x^2\_2<0$

![그림6](https://t1.daumcdn.net/cfile/tistory/992EC4475A4D8A2E35) ![그림7](https://t1.daumcdn.net/cfile/tistory/990593425A4D8D770F) {: style="text-align:center;"}

물론 더 복잡한 경우에는 오른쪽의 그림과 같은 경우도 나올 수 있습니다. 이렇게 실제로는 Non-linear(비선형적인) Decision Boundary를 가지게 되는 경우가 상당히 많은데, 이러한 경우에는 Polynomial(다항식)을 이용하여 Dimension(차수)를 높여 Non-linear Decision Boundary를 표현할 수 있습니다.

***

### 4. Cost Function

#### \[ Cost Function ]

이번에는 Logistic Regression을 풀기위해 필요한 $θ$ 를 구하는 방법에 대해서 알아보도록 하겠습니다. 우리가 직면한 문제는 아래의 그림과 같고 $θ$ 를 고르는 것이 우리가 해야 할 일입니다.

![그림8](https://t1.daumcdn.net/cfile/tistory/99D773385A4DEFFD1F) {: style="text-align:center;"}

앞에서 우리가 배웠던 Linear Regression을 위한 공식은 $J(θ)=\frac{1}{2m}\sum^m\_{i=1}(h\_θ(x^{(i)})−y^{(i)})^2$ 와 같으며 우리는 이를 간단히 아래와 같이 적을 수 있습니다.

$$Cost(h_θ(x),y)=\frac{1}{2}(h_θ(x)−y)^2$$

그리고 Logistic Regression 문제를 위해 $h\_θ(x)=\frac{1}{1+e^{−θ^Tx\}}$ 를 대입하면 비용함수가 구해질 것 같지만 우리는 이것을 사용할 수 없습니다.

그 이유는 위의 과정에 따라 대입한 비용함수 $J(θ)$ 는 아래의 그림과 같은 Non-Convex 함수이기 때문입니다. Linear Regression의 비용함수는 Convex = Single bow-shaped 구조로 Gradient Descent를 실행하면 Global Minimum으로 수렴함을 보장했었지만 Logistic Regression의 비용함수는 그것을 보장하지 못합니다.

![그림9](https://t1.daumcdn.net/cfile/tistory/99A6A64E5A4DF3EA23) {: style="text-align:center"}

\


#### \[ Logistic Regression Cost Function ]

그래서 Logistic Regression을 위한 비용함수는 다음과 같이 정의합니다.

$$Cost(h_θ(x),y)=\begin{cases}−log(h_θ(x)) & \text{amp; if $y$=1} \\\ −log(1−h_θ(x)) & \text{amp; if $y$=0}\end{cases}$$

여기서 0\~1범위의 $h\_θ(x)$가 Input으로 오면 비용함수가 나타납니다. 비용함수는 위에서 보이듯이 $y=1$인 경우와 $y=0$인 경우가 다른 함수로 구분되어 있는데, $y=1$ 인 경우부터 살펴보도록 하겠습니다.

![그림10](https://t1.daumcdn.net/cfile/tistory/996728375A4DF89926) {: style="text-align:center"}

$y=1$인 경우는 $h\_θ(x)=1$ 이면 $Cost=0$ 이지만 $h\_θ(x)\to0$ 이면 $Cost\to∞$ 임을 알 수 있습니다.

이것이 의미하는 것을 이해하는 것이 꽤나 중요한데, Tumor 문제에서 $h\_θ(x)=1$ 이라면 의사는 그 Tumor가 Malignant일 확률이 거의 100%라고 얘기를 해줄 것이고 그때의 비용은 0입니다. 하지만 $h\_θ(x)\to0$ 인 상황에서 의사가 Malignant 일 확률이 매우 높다고 얘기를 하면 잘못된 예측을 한 것이므로 $Cost\to∞$ 로 매우 큰 비용을 들이는 Penalty를 지불해야 함을 의미합니다.

![그림11](https://t1.daumcdn.net/cfile/tistory/99336A3F5A4DFB8E07) {: style="text-align:center"}

반대로 $y=0$인 경우는 그래프가 약간 다르게 그려집니다. $h\_θ(x)\to1$ 이면 $Cost\to∞$ 이며 $h\_θ(x)=0$ 이면 $Cost=0$ 임을 알 수 있는데, 이것이 의미하는 것을 아는 것 역시 중요합니다.

$h\_θ(x)\to1$ 인 경우는 입력 $X$가 $y=1$ 인 Class에 속하는 것이 확실하다고 판단을 하는 상황입니다. 하지만 위 그래프는 $y=0$인 Class이므로 예측은 완전히 잘못되었으며 그에 대한 Penalty가 $Cost\to∞$ 로 보아 매우 큼을 알 수 있습니다. 반대로 $h\_θ(x)=0$ 인 경우는 $y=1$ Class가 아니라 $y=0$ 이라고 예측을 올바르게 하고 있으므로 비용이 0임을 알 수 있습니다.

\


#### \[ Simplified cost function and Gradient Descent ]

위에서 우리가 배운 비용함수는 $y=1$인 경우와 $y=0$인 경우로 나뉘어졌기 때문에 보기에 불편하지만 이를 하나의 식으로 완전히 같은 함수를 표현할 수 있습니다.

$$Cost(h_θ(x),y)=−\color{red}{y}log(h_θ(x))−\color{blue}{(1-y)}log(1−h_θ(x))$$

물론 다른 비용함수들도 많지만 통계학적으로 다른 모델들에 대하여 Parameter $θ$ 를 구하는 가장 효율적인 함수라고 합니다. 또한 **Convex(볼록)함수**이기 때문에 Logistic Regression Model을 해결하기 위해 대부분이 사람들이 이 함수를 사용합니다.

$$J(θ)=\frac{1}{m}\sum_{i=1}^mCost(h_θ(x^{(i)}),y^{(i)})=−\frac{1}{m}\sum_{i=1}^m[y^{(i)}logh_θ(x^{(i)})+(1−y^{(i)})log(1−h_θ(x^{(i)}))]$$

이제 위와 같은 비용함수 $J(θ)$를 최소로 만드는 $θ$를 구해야합니다. 만약 Feature들의 집합 $X$가 주어졌을 때, 우리는 $θ$값을 이용하여 $h\_θ(x)$ 를 구할 수 있고 이 값은 $P(y=1 \mid x;θ)$ 로 $y=1$인 클래스에 속할 확률을 의미합니다.

Global Optima가 되는 $θ$ 를 구하기 위해서는 Gradient Descent를 적용해야 하는데 기존의 알고리즘에 $J(θ)$ 만 대입하면 아래와 같은 식이 됩니다.

n개의 Feature가 있는 경우에 $θ$는 nx1차원의 배열이 되고 Gradient Descent는 총 n개의 모든 $θ$에 대하여 각각 진행됩니다.

$J(θ)$ 외에 Linear Regression과 또 다른 하나는 기존의 $h\_θ(x)=θ^Tx$ 에서 $h\_θ(x)=\frac{1}{1+exp(−θ^Tx)}$ 로 바뀌었다는 점입니다. 그러나 진행은 동일하며 Logistic Regression이 정상적으로 작동하는지 확인하는 방법도 $J(θ)$가 줄어드는지 확인하는 Linear Regression과 동일합니다.

하지만 0\~n까지의 n+1번의 반복을 하는 것은 비효율적이므로 _Vector Rise Implementation_을 활용하여 n+1개의 $θ$를 한번에 처리해주고 있습니다. 자세한 내용은 \[여기]\[vectorization]의 For Loop V.S. Vectorization 부분에 자세히 서술되어 있습니다.

마지막으로 남은 것은 _Feature Scaling_을 배워 Gradient Descent의 속도를 높이는 것입니다.

***

### 5. Advanced Optimization

최적화 알고리즘들과 향상된 최적화 개념을 이용하면 Logistic Regression을 더욱 빠르게 만들 수 있고, Feature가 매우 많은 머신 러닝 문제들도 Scale을 크게 하여 해결가능 할 것입니다.

#### \[ Optimization Algorithm ]

Gradient Descent가 하는 일은 $J(θ)$를 최소화시키는 것으로 $J(θ)$를 구하고 $\frac{∂}{∂θ}J(θ)$ 를 계산하는 것입니다. 그리고 이것은 우리의 $θ$ 를 계속해서 Update 시켜줍니다. 물론 Gradient Descent 외에도 우리가 활용할 수 있는 알고리즘들이 몇몇 있습니다.

* Gradient Descent
* Conjugate Gradient
* BFGS
* L-BFGS

이러한 알고리즘들은 다음과 같은 장점/단점을 지닙니다.

* 👍: No need to manually pick $α$
* 👍: Often faster than gradient descent
* 👎: More Complex

Gradient Descent를 제외한 3가지 알고리즘은 자체적으로 알고리즘을 시도하여 자동적으로 좋은 $α$ 를 선택하여 줍니다. 그렇기에 매 Interation 마다 $α$ 가 달라질 수 있으며 최적의 $α$ 를 선택하기 때문에 속도는 빠르지만 이러한 알고리즘은 매우 복잡하여 이해하기에 어렵다는 단점이 있습니다.

***

### 6. Multi-class Classification

#### \[ Multi-class Classification ]

아래의 예시들 처럼 **여러 개의 Class로 분류되는 문제**를 Multi-Class Classification 문제라고 합니다. 앞서서 배운 Class 0 또는 Class 1로 나누는 것을 Binary Classification 그리고 여러 개의 Class로 나누는 것을 Multi-Class Classification 이라고 하며 이를 그림으로 나타내면 아래와 같습니다.

* Email foldering/tagging: Work, Friends, Family, Hobby
* Medical diagrams: Not ill, Cold, Flu
* Weather: Sunny, Cloudy, Rain, Snow

![그림12](https://t1.daumcdn.net/cfile/tistory/9960B1445A4E23FC2A) {: style="text-align:center"}\


#### \[ One-vs-all(one-vs-rest) ]

아래의 예시처럼 3개의 Class가 있는 Data Set이 주어졌다고 할 때, 우리는 Multi-Class Classification 문제를 해결하기 위해 One-vs-all(one-vs-rest) 알고리즘을 사용할 것입니다.

이 알고리즘은 **n개의 클래스가 있는 원래의 문제를 n개의 Binary Classification 문제로 바꾸어 해결**할 것입니다.

* △가 Positive Value 나머지는 Negative Value $\quad \to h^{(1)}\_θ$ (y가 1에 속할 확률)
* ㅁ가 Positive Value 나머지는 Negative Value $\quad \to h^{(2)}\_θ$ (y가 2에 속할 확률)
* ㅇ가 Positive Value 나머지는 Negative Value $\quad \to h^{(3)}\_θ$ (y가 3에 속할 확률)

![그림13](https://t1.daumcdn.net/cfile/tistory/99EEED4B5A4E25A42A) {: style="text-align:center"}

즉, 이 문제는 $y=i$ 일 확률을 예측하는 Logistic Regression Classifier $h^{(i)}\_θ(x)$ 를 학습하는 것으로 **새로운 Input x가 주어지면 x에 대한 3개의 Classifier를 적용하여 최대 확률을 갖는 Class를 선택**하는 것입니다.
