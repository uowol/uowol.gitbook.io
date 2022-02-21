# Multivariate Linear Regression

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/35)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Multivariate Linear Regression에 대해서 알아보도록 하겠습니다.

### 1. Multiple Features(Variables)

#### \[ Multiple Features ]

기존에는 하나의 X로 Y를 예측하는 상황이였습니다. 하지만 실제 현실에서는 다양한 변수들 즉, 여러 개의 X를 통하여 Y를 예측하는 경우의 문제가 대부분입니다. 그러므로 우리는 4개의 Features를 가지는 문제에 대해서 알아보도록 하겠습니다. 아래의 그림에서는 Size, Number of bedrooms, Number of floors, Age of home이라는 4가지 변수를 통해서 Price를 예측하고 있습니다. 앞으로 이러한 다중 변수 상황에 대비하기위해 표기법을 정의하고 넘어가도록 하겠습니다.

![그림1](https://t1.daumcdn.net/cfile/tistory/99D588345A489AFC01)

#### \[ Notation(표기법) ]

* $n$ : number of features
* $x^{(i)}$ : input (features) variable or $i^th$ training example
* $x^i\_j$ : value of feature j in ith training example

예를 들어 $x^{(3)}\_2$은 3이 되고, $x^{(2)}\_1$는 1416이 되며 $x^{(2)}=\begin{bmatrix} 1416 \\\ 3 \\\ 2 \\\ 40 \end{bmatrix}$의 4차원 배열이 됩니다. 이러한 정의를 따라서 기존의 가설함수였던 $h\_θ(x)=θ\_0+θ\_1x$는

$$h_θ(x)=θ_0+θ_1x^1+θ_2x^2+...+θ_nx^n$$

로 변하게 되었습니다.

예를 들어 집값 문제에서의 가설함수가 $h\_θ(x)=80+0.1x^1+0.01x^2+3x^3−2x^4$ 와 같이 표현되었다고 할 때 우리는 직관적으로 80은 상수이므로 집의 기본값이며, $θ\_1$=0.1은 제곱미터당 가격, $θ\_2$=0.01은 층 당 가격 등으로 볼 수 있으며 $x^4$ 는 감소에 영향을 주는 변수이므로 age에 해당하는 것으로 이해할 수 있습니다.

$X$ 의 벡터 $X=\begin{bmatrix} x0 \\\ x1 \\\ ... \\\ x\_n \end{bmatrix}$ 로 표현가능하고, $θ^T$ 의 벡터 $θ^T=\begin{bmatrix}θ\_0 & θ\_1 & ... & θ\_n\end{bmatrix}$ 로 표현가능하므로 가설함수는 아래와 같이 표현할 수 있습니다. ( $θ^T$ 는 $θ$ 의 벡터에 대한 전치행렬)

$$h_θ(x)=\begin{bmatrix}θ_0 & θ_1 & ... & θ_n\end{bmatrix}\begin{bmatrix} x0 \\\ x1 \\\ ... \\\ x_n \end{bmatrix} = \theta^Tx$$

\


#### \[ Gradient Descent for Multiple Features ]

앞에서는 Multiple Variables를 갖는 경우의 가설함수에 대해서 알아보았고 이제 우리는 $θ\_0,θ\_1,...θ\_n$ 과 같은 Parameter들을 어떻게 맞추는지에 대해서 알아볼 것입니다. 기존에 feature가 1개인 경우에는 아래와 같이 $θ\_0,θ\_1$ 만 존재하는 아래와 같은 Gradient Descent를 진행하면 되었습니다.

하지만 Multivariate인 경우 즉, $n≥1$인 경우에는 아래와 같은 Gradient Descent를 진행하면 됩니다.

그리고 위 식을 각각의 $θ$ 에 대해서 풀어서 적으면 아래와 같습니다.

수식 출처: [\[Machine Learning\] Multivariate Linear Regression(망나니개발자)](https://mangkyu.tistory.com/35)

***

### 2. Feature Scaling

#### \[ Feature Scaling ]

Feature Scaling에 대한 아이디어는 Multiple Features를 갖는 문제에서 각각의 Feature들이 비슷한 Scale 즉, **비슷하거나 같은 범위를 갖는다면 Gradient Discent가 더욱 빨리 Optima로 수렴가능하다**는 생각에서 시작되었습니다.

아래의 그림에서 왼쪽과 같이 2개의 Feautre가 갖는 범위의 차이가 많이 나는 경우에는 원에서 많이 찌그러진 타원의 모양을 갖게 될 것이고 Global Optima를 구하는데 오랜 시간이 소모될 것입니다. 하지만 오른쪽 그림과 같이 각 Feature의 값을 최대값 or 최대값-최소값 등과 같은 값으로 나누어준 값으로 치환하여 계산한다면 타원보다 원에 가까운 모양이 될 것이고 더 적은 Gradient Discent 연산을 통해 Global Optima에 도달하게 될 것입니다.

![그림2](https://t1.daumcdn.net/cfile/tistory/992B3D4E5A48D7F836)

***

### 3. Learning Rate

#### \[ Learning Rate ]

이번 장은 Learning Rate $α$가 중심이 되는 Debugging 작업으로 Gradient Descent가 잘 돌아가도록 하기 위한 방법과 $α$를 고르는 방법에 대해서 알아보도록 하겠습니다.

Gradient Descent의 역할은 비용함수 $J(θ)$ 를 최소화시키는 $θ$ 를 찾는 것으로 이것에 대한 디버깅작업은 Gradient Descent를 할 때마다 변화하는 $J(θ)$ 를 그리며 올바르게 $J(θ)$ 가 감소하는지를 확인하는 작업입니다. 올바르게 동작하는 Gradient Descent에 대한 $J(θ)$는 아래의 그림과 같은 모양이 될 것입니다.

![그림3](https://t1.daumcdn.net/cfile/tistory/992FAA4C5A48CC380D) {: style="text-align:center;"}

위 그래프에서 x축은 반복의 횟수로 Gradient Descent가 정상적으로 작동한다면 $J(θ)$ 는 계속해서 감소할 것이고, 반복이 진행될수록 $J(θ)$ 의 접선의 기울기가 0으로 수렴하게될 것입니다.

우리는 수렴을 위해서 몇번의 반복 작업이 필요한지 알 수 없으므로 보통은 그래프를 그리며 반복 횟수의 증가에 따라서 $J(θ)$ 를 그리며 이것이 수렴하는지를 확인합니다. 또는 수렴여부를 자동으로 검사해주는 알고리즘인 _Automatic Convergence Test_를 활용하여 수렴여부를 파악할수도 있습니다.

\


#### \[ Automatic Convergence Test ]

앞에서 설명한대로 _Automatic Convergence Test_는 수렴여부를 자동으로 판단해주는 알고리즘으로 수렴했는지를 판단하는 기준은 $J(θ)$의 감소량이 어떤 작은 값 E보다 작을 때를 기준으로 수렴했다고 판단합니다.

일반적으로 E는 $10^−3$ 이지만 문제에 따라서 달라지므로 E를 정하는 것 조차도 또다른 문제가 됩니다. 그러므로 이 알고리즘을 활용하는 것 보다는 그래프를 그려 확인하는 편이 좋습니다.

$$Declare \quad Convergence \quad if \quad J(θ) \quad decreases \quad by \quad less \quad than \quad 10^{−3}$$

아래의 왼쪽 그림처럼 $J(θ)$ 가 증가하는 경우에는 Gradient Descent가 잘못 작동하고 있으며 $J(θ)$ 가 증가하는 이유는 Learning Rate $α$ 의 값이 너무 커서 오른쪽 그림과 같이 증가하는 까닭이므로 이를 해결하기 위해서는 $α$를 줄여야 한다는 것을 알 수 있습니다.

![그림4](https://t1.daumcdn.net/cfile/tistory/992B3C4A5A48D33B1D) ![그림5](https://t1.daumcdn.net/cfile/tistory/99DB36485A48D2BC15)

또는 아래 그림과 같이 증가와 감소를 반복하는 경우에도 Learning Rate α 의 값을 줄여주면 해결됩니다.

![그림6](https://t1.daumcdn.net/cfile/tistory/99CB57425A48D4B032) {: style="text-align:center"}

어떤 수학자의 증명에 따르면 $α$ 가 충분히 작은 경우에 $J(θ)$ 는 매회 반복시에 항상 줄어들게 되어있습니다. 그러므로 $J(θ)$ 가 줄어들지 않는 경우에는 $α$ 를 줄이면 되고, 물론 $α$ 가 너무 작은 경우에는 Gradient Descent가 천천히 줄어들게 되므로 적당히 작은 $α$ 를 갖게 해주어야 합니다. $α$ 를 선택할 때에는 0.001 - 0.003 - 0.01 - 0.03 - 0.1 - 0.3 - 1 과 같이 **3배수 꼴로 활용해주는게 가장 효율적**입니다.

***

### 4. Features and Polynomial Regression

이번에는 Feature를 선택하는 방법과 적절한 Feature의 선택으로 Hypthesis Function을 개선하여 강력한 학습 알고리즘을 만드는 방법에 대해서 알아보도록 하겠습니다.

#### \[ New Feature ]

아래의 그림과 같이 집의 가로 길이와 세로 길이에 대한 값이 주어진 경우에 가격을 예측하는 경우라고 가정을 합시다.

그렇다면 우리는 $h\_θ(x)=θ\_0+θ\_1×(frontage)+θ\_2×(depth)$ 와 같은 가설함수를 세울 수 있습니다. 하지만 이렇게 가로 길이와 세로 길이를 각각의 Feature로 사용하는 것은 비효율적이므로 Area라는 $x\_1=(area)=(frontage)×(depth)$ 와 같은 새로운 Feature를 만들어서 가설함수를 단순화시키는 것이 훨씬 효율적입니다. 이러한 방법으로 새로운 Feature를 만들면 더 좋은 Model을 얻을 수 있습니다.

![그림7](https://thetascienceblog.files.wordpress.com/2016/07/untitled.png) {: style="text-align:center"}\


#### \[ Polynomial Regression ]

Feature를 선택하는 것과 밀접하게 관련된 것으로 선형 회귀를 이용하여 복잡한 비선형함수에 적용하는 다항 회귀(Polynomial Regression)이 있습니다.

예를 들어 아래의 그림과 같은 Data set이 있다고 할 때 우리는 $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2x^2\_1$와 같은 가설함수를 세울 수 있습니다. 물론 이 가설함수는 잘 맞는 것 처럼 보이지만 뒤로 갈수록 감소하므로 우리가 원하는 가설함수가 아님을 파악할 수 있습니다.

그래서 우리는 이를 개선한 $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2x^3\_1+θ\_3x^3\_1$ 3차식 가설함수를 생각해낼 수 있습니다. 여기서 $x^3\_1$ 이 되는 경우는 원래의 $x\_1$ 의 범위가 1~~1000이라면 1~~1000000000이 되므로 **Feature Scaling**을 반드시 해주어야 합니다.

그 외에도 우리는 $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2\sqrt{x\_1}$ 과 같은 좋은 가설함수도 생각해낼 수 있습니다. 이처럼 Feature가 많은 경우에 어떠한 Feature를 사용할지를 고르는 알고리즘을 다음 장에서 배울 것입니다.

* $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2x^2\_1$
* $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2x^3\_1+θ\_3x^3\_1$
* $h\_θ(x)=θ\_0+θ\_1x\_1+θ\_2\sqrt{x\_1}$

![그림8](https://t1.daumcdn.net/cfile/tistory/9903B1395A48E3331C)

***

### 5. Normal Equation

이번에는 특정한 선형 회귀 문제에서 **$θ$ 를 구하는 효과적인 방법**에 대해서 알아보도록 하겠습니다.

#### \[ Normal Equation ]

기존에 우리가 배웠던 Gradient Descent는 Optima로 가기 위해 여러 번의 연산을 수행해야 하는 번거로움이 있습니다.

하지만 특정한 선형 회귀 문제에서 **Analytically 하게 단 한번의 연산으로 $θ$ 를 구하는 효과적인 방법**이 있는데, 그것이 바로 **Normal Equation** 입니다.

직관적으로 Feature가 1개인 즉, 2차함수의 꼴( $y=\theta\_0+\theta\_1x$, 우리가 초점을 맞춰야 하는 것은 $\theta$ )인 $J(θ)$ 의 최소값을 구할 때 우리는 직관적으로 $J(θ)$ 를 미분하여 극소값을 찾아냅니다. 하지만 실제 문제에서 $θ$ 는 실수가 아니라 n+1차원의 배열이기 때문에 $J(θ)$ 는 $θ\_0 .... θ\_n$ 벡터의 함수가 됩니다.

그러므로 이러한 $J(θ)$ 의 최소값을 구하기 위해서는 **각 $θ$ 에 대하여 편미분하여 0이 되는 각각의 $θ$ 를 구해야 합니다.**

$$\theta \in \Bbb{R}^{n+1} \quad J(θ_0,θ_1...,θ_n)=\frac{1}{2m}\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})^2$$

$$\frac{∂}{∂θ_j}J(θ)=~.... ~=0 \quad(for~every~j~and~solve~for~θ_0,θ_1...,θ_n)$$

\


#### \[ Example ]

예를 들어 아래의 그림과 같이 m=4(# of examples)인 Training Set이 주어졌다고 할 때, 가장 먼저 해야하는 일은 모든 값이 1인 Feature $x\_0$ 를 추가하는 것입니다. 그리고 각각의 m, n+1 차원의 배열 X 와 m차원 배열 Y를 아래와 같은 배열로 뽑아낼 수 있는데, 여기서 우리가 원하는 값이 $θ^T=(X^TX)^{−1}X^Ty$ 이므로 이를 계산해주면 됩니다.

![그림9](https://t1.daumcdn.net/cfile/tistory/9976773F5A4C59CC30)

일반적인 상황에서 $(x^{(1)},y^{(1)}),...,(x^{(m)},y^{(m)})$ m 개의 Examples와 n개의 Feature이 주어진 Training Set에서 위의 예시에서 한 것처럼 m, n+1 차원의 Design Matrix인 X를 만들고, m차원의 행렬 Y를 만들어 이를 계산하면 됩니다.

$θ=(X^TX)^{−1}X^Ty$ 의 식을 계산하면 바로 $θ^T$ 를 얻을 수 있으므로 반복된 작업이 필요하지 않으며, **Gradient Descent를 사용하지 않으므로 Feature Scaling이 필요하지 않습니다.**

\


#### \[ Gradient Descent VS Normal Equation ]

* eg. Use gd if $n≥10,000$

| : Gradient Descent :          | : Normal Equation :                     |
| ----------------------------- | --------------------------------------- |
| Need to choose $α$            | No need to choose $α$                   |
| Need many iterations          | No need to iterate                      |
| Works well whene $n$ is large | Slow if $n$ is very large               |
| $O(kn^2)$                     | $O(n^3)$ to calculate $(X^TX)^{−1}X^Ty$ |

\


#### \[ non-invertibility Normal Equation ]

$θ$를 구하기 위해서 필요한 계산인 $(X^TX)^{−1}X^Ty$ 를 해야 하는데 만약 역행렬 $(X^TX)^{−1}$ 이 존재하지 않는다면 어떻게 해야 될까요?

역행렬이 존재하지 않는 이유는 크게 2가지로 나뉘어집니다.

* 불필요한 Feature를 가지고 있는 경우 -> 불필요한 Feature 제거
* 많은 Feature를 가지고 학습 알고리즘을 진행하는 경우 -> Feature 제거 or Regularization

예를 들어 어떤 Training Set에서 $x1=(feet)^2,x2=(meter)^2$ 과 같은 Feature를 가지고 있다고 할 때 2개의 Feature은 독립적인 것으로 보일 수 있지만 실제로는 $1meter = 3.28feet와$ 같으므로 동일한 데이터가 중복되어 있습니다. 그리고 이렇게 불필요한 Feature를 가지고 있는 경우에 역행렬이 존재하지 않을 수 있습니다.

또한 Training Example의 개수들에 비해 Feature가 너무 많은 경우 즉, $m ≥ n$ 인 경우에도 역행렬이 존재하지 않을 수 있는데, 이러한 경우에는 Feature들을 몇개 지우거나 \*\*Regularization(정규화)\*\*을 하여 이러한 문제를 해결할 수 있습니다.

그러므로 역행렬이 없는 경우에는 서로 종속성이 있는 Feature들이 존재하는지 검사하여 존재하면 제거하고 그렇지 않은 경우에는 불필요한 Feature들을 제거하거나 Regularization을 하면 됩니다.
