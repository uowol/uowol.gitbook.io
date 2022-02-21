# Gradient Descent

### 참고

[망나니개발자님의 블로그](https://mangkyu.tistory.com/31?category=767742)

```
본 내용은 망나니개발자님이 Coursera에서 Andrew ng 의 Machine Learning(기계학습, 머신러닝)을 수강한 내용을 정리한 것을 바탕으로 작성된 글입니다. 
```

이번 포스팅에서는 Gradient Descent(경사 하강법, 기울기 하강법)에 대해서 알아보도록 하겠습니다.

### 1. Gradient Descent(경사하강법)

#### \[ Gradient Descent ]

Gradient Descent Algorithm은 **Cost Function $J(θ\_0,θ\_1)$ 을 최소로 만드는 $θ\_0,θ\_1$ 을 구하는 알고리즘**으로 Linear Regression뿐만 아니라 머신러닝(기계학습)에서 전반적으로 사용되는 알고리즘입니다.

Gradient Descent는 먼저 $θ\_0,θ\_1$ 에 대한 _임의의 초기값 $(x, y)$_ 로 시작합니다. 그리고 최소의 $J(θ\_0,θ\_1)$ 을 찾을 때 까지 $θ\_0,θ\_1$ 을 변경시킵니다. 즉, 이 알고리즘은 임의의 초기값을 기준으로 최소가 되는 점을 찾아나갑니다.

![그림1](https://t1.daumcdn.net/cfile/tistory/99A123355A3A2DAF12)

Gradient Descent Algorithm을 수학적으로 정의하면 다음과 같습니다.

repeat until convergence{

$$θ_j:=θ_j−α\frac{∂}{∂θ_j}J(θ_0,θ_1)$$

}

* $:=$ : Assignment Operator (대입 연산자)
* $α$ : Learning Rate (학습 속도)
* $\frac{∂}{∂θ\_j}J(θ\_0,θ\_1)$ : Derivative Term (미분 계수)

여기서 **$:=$** 는 _대입 연산자_로 **$θ\_j$ 에 $θ\_j−α□$ 을 대입하겠다는 의미**입니다.

**$α$** 는 _Learning Rate_로 위의 그림에서처럼 **언덕에서 내려갈 때 얼마나 큰 걸음으로 걸을 것인가를 나타내는 양의 상수**이므로 $α$ 가 클수록 한 Step에 움직이는 길이가 길어집니다.

**$\frac{∂}{∂θ\_j}J(θ\_0,θ\_1)$** 는 **비용함수를 $θ$에 대해 미분한 함수**입니다. 미분해주는 값은 $J(θ\_0,θ\_1)$ 즉, 비용함수로 $θ\_0,θ\_1$ 총 2가지 변수에 의해 영향을 받고 있습니다.

우리는 이러한 대입의 과정을 지속해주어야 하는데, 아래의 오른쪽 그림(글쓴이: 원본 글에서도 찾아볼 수 없습니다.) 처럼 대입을 하면 $θ\_1$의 값을 대입할 때 비용함수가 영향을 받으므로 왼쪽의 그림(글쓴이: 마찬가지로 원본 글에서 찾아볼 수 없습니다.) 처럼 **Simultaneous 하게 동시에 Update를 해주어야 합니다.**

지금부터 경사 하강 알고리즘을 구성하는 요소들에서 Learning Rate $α$ 가 무엇을 하는지 그리고 왜 미분계수와 $α$ 를 곱한 $α\frac{∂}{∂θ\_j}J(θ\_0,θ\_1)$를 이용하는지 이해를 돕기위해 하나의 Parameter $θ\_1$ 만을 갖는 경우에 대해서 알아보도록 하겠습니다.

\


#### \[ Derivative Term(미분 계수) ]

우리는 결국 $J(θ\_1)$이 최소가 되는 실수 $θ\_1$ 을 구해야 합니다.

아래와 같은 그림에서 파랑색의 $θ\_1$ 을 초기값으로 최소값을 찾아나간다고 할 때, $\frac{∂}{∂θ\_j}J(θ\_1)$ 부분은 **미분계수(한 점에서의 기울기 값)** 즉, 초록색 직선의 기울기에 해당합니다. 또한 $α$ 가 양수이므로 $α\frac{∂}{∂θ\_j}J(θ\_1)$ 도 양수(Positive Number)가 되어 $θ$ 가 점점 줄어들며 최소로 가는 모습임을 알 수 있습니다. 그리고 이것이 바로 기울기 하강(Negative Slope)입니다.

![그림2](https://t1.daumcdn.net/cfile/tistory/99C901415A3A564B1E) {: style="text-align:center;"}

$θ\_1$ 이 좌측에 있는 경우에는 아래의 그림과 같이 미분계수가 음이 되고 $α$ 가 양수이므로 $α\frac{∂}{∂θ\_j}J(θ\_1)$ 이 음수(Negative Number)가 되어 전체는 양수가 되므로 $θ$ 가 점점 증가하며 최소로 가는 모습임을 알 수 있습니다. 그리고 이것이 바로 기울기 상승(Positive Slope)입니다

![그림3](https://t1.daumcdn.net/cfile/tistory/9988033F5A3A57E21C) {: style="text-align:center;"}\


#### \[ Learning Rate(학습 속도) ]

그 다음으로 우리는 **움직이는 보폭의 크기인 Learning Rate $α$** 에 대해서 알아보아야 하는데, $α$ 의 값이 큰 경우와 작은 경우로 나누어 각각 어떤 문제를 발생시키는지 알아보겠습니다.

왼쪽의 그림과 같이 Learning Rate가 너무 작은 경우에는 최소값에 도달하기 위해 상당히 많은 연산을 필요로 하게됩니다. 그렇다고 Learning Rate가 너무 크면, (공식을 보고 예측을 해보면) 우리는 매우 큰 거리로 이동하므로 반대쪽 값으로 넘어가게 되며 최소값으로부터 점점 멀어지는 것을 확인할 수 있습니다.

그래서 우리는 Learning Rate를 적당한 값으로 설정해주어야 합니다.

![그림4](https://t1.daumcdn.net/cfile/tistory/99287D425A3A5E501F)

(글쓴이: 아래 내용은 개인적인 의견을 반영하여 원본 글과는 조금 다르게 작성하였습니다.)

마침내 우리는 왜 Learning Rate $α$ 와 Derivate Term $\frac{∂}{∂θ\_j}J(θ\_1)$ 을 함께 사용하는지에 대해 이해할 수 있습니다.

우리는 Dericate Term을 사용하여 최소값을 찾아갈 수 있고, 그 과정에서 적절한 Learning Rate를 설정해 줌으로써 조금 더 수월하게 진행할 수 있습니다.

\


#### \[ Convergence(수렴) ]

그렇다면 Gradient descent이 수렴하여 연산을 종료하는 시간은 언제일까요?

그것은 바로 **$\frac{∂}{∂θ\_j}J(θ\_1)$이 0이 되어 $θ\_1$의 값이 더 이상 변하지 않을 경우**입니다. 즉, $θ\_1$ 이 이미 최적의 값(Local Optima)이여서 접선의 기울기가 0이고, Cost Function $J(θ\_1)$이 최소가 되는 상황입니다.

그러나 언제나 깔끔하게 수렴하여 연산이 종료되지는 않습니다. 간혹 최소값으로 수렴하지 않고 제자리에서 진동하는 경우가 발생합니다.

이를 프로그램으로 구현한다면 연산이 종료되지 않는 문제가 발생하는데, 그것을 해결하기 위해선 **충분히 만족스러운 결과의 척도나 연산 횟수를 설정하여 연산이 어느정도 진행되었을 때 종료**시켜주는 것이 좋습니다.

![그림5](https://t1.daumcdn.net/cfile/tistory/994D79365A3A65BC11) {: style="text-align:center;"}

***

### 2. Gradient Descent for Linear Regression

#### \[ Gradient Descent for Linear Regression ]

이제 우리는 아래의 그림과 같이 가설함수와 비용함수 그리고 최적의 비용함수를 갖는 $θ$를 찾기 위한 Gradient Descent 모두를 배웠습니다. 그러므로 이것들을 이용하여 우리의 데이터들에 맞는 직선(최적의 가설 함수)을 구해주기만 하면 됩니다.

![그림6](https://t1.daumcdn.net/cfile/tistory/99DDC0445A3A6A4418)

즉, Gradient Descent를 $J(θ\_0,θ\_1)$ 에 적용하여 Cost Function을 최소화시킬 것입니다. 그리고 이 과정에서 가장 중요한 것은 Gradient Descent Algorithm에서 $\frac{∂}{∂θ\_j}J(θ\_0,θ\_1)$ 입니다. 원래의 예시에서는 $θ\_0,θ\_1$ 두개의 값을 가지므로 2개의 함수가 각각 나오게되고 미분을 직접 해보면 아래와 같이 나오게 됩니다.

$$\frac{∂}{∂θ_j}J(θ_0,θ_1)~=~\frac{∂}{∂θ_j}[\frac{1}{2m}\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})^2]$$

$$=~\frac{∂}{∂θ_j}[\frac{1}{2m}\sum_{i=1}^m(θ_0+θ_1x^{(i)}−y^{(i)})^2]$$

그리고 이것을 풀어서 계산하면 다음과 같습니다.

$$j=0:\qquad\frac{∂}{∂θ_j}J(θ_0,θ_1)=m\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})$$

$$j=1:\qquad\frac{∂}{∂θ_j}J(θ_0,θ_1)=m\sum_{i=1}^m(h_θ(x^{(i)})−y^{(i)})x^{(i)}$$

그리고 이것을 Gradient descent algorithm에 적용하면 아래와 같습니다.

![그림7](https://t1.daumcdn.net/cfile/tistory/9956CE3F5A3A6F4235) {: style="text-align:center;"}

앞에서 설명하였듯이 등고선이 복잡한 경우에는 아래의 그림과 같이 Global Optimal(실제 최소값) Local Optimal(특정 지역의 최소값)이 존재하여 초기값의 위치에 따라서 최적의 최소값이 달리집니다. 그러므로 초기값을 무엇으로 잡는지에 따라 우리가 얻게되는 $θ\_0,θ\_1$의 값이 달리집니다.

![그림8](https://t1.daumcdn.net/cfile/tistory/99A0E3335A3A6FF42C) ![그림9](https://t1.daumcdn.net/cfile/tistory/99A1694D5A3A70FE1B) {: style="text-align:center;"}

하지만 선형 회귀 Linear Regression의 Cost Function은 Convex Function(볼록 함수) 중에서도 위의 오른쪽 그림과 같은 Bowl-Shaped Function을 갖게 되고 Local Optima(지역적 최소값) 없이 Global Optima(전역적 최소값)만 갖게되므로 **Linear Regression은 무조건 Global Optima로 수렴하게 되어있습니다.** 그리고 이러한 규칙을 따라서 계속 Gradient Descent를 진행하면 빨간 점들을 지나서 최소값에 도달하게 됩니다

![그림10](https://t1.daumcdn.net/cfile/tistory/99DF4C4A5A3A716D30)

\


#### \[ Batch Gradient Descent ]

우리가 배운 Gradient Descent는 Batch Gradient Descent로 Batch의 뜻은 다음과 같습니다.

```
   Batch: Each step of gradient descent uses all the training examples
```

즉, Gradient Descent 알고리즘을 사용하면서 **매 단계마다 모든 Training Set를 활용한다**는 말입니다. 실제로 우리는 Gradient Descent에서 미분계수를 계산할 때 $\sum^m\_{i=1}$ 을 사용하여 모든 Training Set에 대하여 계산을 해줍니다. 물론 모든 Data Set를 사용하지 않는 알고리즘도 존재합니다.
