# 표본분포에 대한 사설과 카이제곱분포

이번엔 여러 가지 통계적 추론에서 다양하게 이용되는 정규모집단에서의 몇 가지 중요한 표본분포에 대해 알아보겠습니다.

```
이 포스팅은 영지문화사의 '일반통계학' 책을 참고하여 작성되었습니다.
```

### 0. 서론

정규분포 $N(\mu, \sigma^2)$ 으로부터의 랜덤표본을 $X\_1, \cdots, X\_n$ 이라 할 때, 표본분산은 다음과 같이 구할 수 있습니다.

$$S^2 = \frac{1}{n-1}\sum_{i=1}^n(X_i - \bar X)^2$$

그리고 표본분산 $S^2$ 의 표본분포는 $\sigma^2$ 의 추론에 유용하게 쓰입니다.

모수의 추론에는 모분산 $\sigma^2$ 이 자주 활용되지만 실제로 $\sigma^2$ 를 알고 있는 경우는 굉장히 드물기 때문에 주로 표본분산 $S$ 를 이용하곤 합니다.

따라서, 지금부터 $\sigma^2$ 대신 $S^2$ 로 모수를 추론하는 방법과 $S^2$ 에 관계되는 여러가지 분포를 살펴보도록 하겠습니다.

총 카이제곱분포, t분포, F분포 이렇게 세 가지 분포를 다룰 예정이고, 첫 포스팅에선 카이제곱분포에 대해 다뤄보겠습니다 :)

\-> \[1. 카이제곱분포]\[카이] <-

\[2. t분포]\[티]

\[3. F분포]\[엪]

***

### 1. 카이제곱분포 ($\chi^2$ 분포)

#### \[ 카이제곱분포 ]

확률변수 $Z\_1, \cdots, Z\_k$ 이 표준정규분포 $N(0, 1)$ 의 랜덤표본일 때,

$$Z_1^2 + \cdots + Z_k^2$$

의 분포를 자유도(해방도, degrees of freedom) k인 카이제곱분포라고 합니다.

이 때, 기호로서

$$Z_1^2 + \cdots + Z_k^2 \sim \chi^2(k)$$

로 나타냅니다.

\


#### \[ 카이제곱분포의 형태 ]

카이제곱분포의 모양은 자유도에 따라 다르지만 대략적인 형태는 아래와 같습니다.

&#x20;{:style="text-align:center;"}

그림과 같이 카이제곱분포의 확률이 왼쪽에 모여있고 오른쪽으로 긴 꼬리를 갖는 이유는 $Z\_1^2 + \cdots + Z\_k^2$ 에서 $Z\_i$ 가 주로 0 근처에 분포하는 확률변수이기 때문입니다.

카이제곱분포의 확률밀도함수(pdf)를 구하는 것은 지금 다루고 있는 수준을 넘으므로 넘어가겠습니다.

중요한 것은, 표준정규분포에서 $P(Z \ge z\_\alpha) = \alpha$ 인 $z\_\alpha$ 값들이 이미 계산되어 있던 것처럼, 카이제곱분포 또한 각 자유도 $k$ 에 따른 $(1-\alpha)$ 분위수가 구해져있습니다.

자유도가 $k$ 인 카이제곱분포의 $(1-\alpha)$ 분위수를 흔히 $\chi^2\_\alpha(k)$ 로 나타냅니다.

그리고, 표준정규분포를 따르는 확률변수를 $Z$ 로 나타낸 것과 같이, 자유도가 $k$ 인 카이제곱분포를 따르는 확률변수는 $V$ 로 나타냅니다.

$$P\{V \ge \chi^2_\alpha(k)\}=\alpha, \quad V \sim \chi^2(k)$$

\


#### \[ 카이제곱분포의 가법성 ]

두 확률변수가 서로 독립이고 각각 카이제곱분포를 따를 때 이들의 합도 카이제곱분포를 따릅니다.

$$$
\begin{array}{l} V_1 \sim \chi^2(k_1)\\ V_2 \sim \chi^2(k_2)\\ V_1 \text{과 } V_2 \text{가 서로 독립} \end{array} \right\} \Rightarrow V_1 + V_2 \sim \chi^2(k_1 + k_2)$$ 카이제곱의 이러한 성질을 카이제곱의 가법성이라고 합니다. <br> ### [ 정규모집단에서의 표본분산의 분포 ] 이번엔 정규모집단에서의 표본분산의 분포에 대하여 생각해보겠습니다. $X_1, \cdots, X_n$ 을 정규분포 $N(\mu, \sigma^2)$ 에서의 랜덤표본이라고 할 때, $$\frac{X_i - \mu}{\sigma} \sim N(0,1)\text{이고 서로 독립} (i=1, \cdots, n)$$ 이므로 카이제곱분포의 정의로부터 $$\sum_{i=1}^n(\frac{X_i - \mu}{\sigma})^2 = \chi^2(n)$$ 이 성립합니다. 그런데, $$\sum_{i=1}^n(\frac{X_i - \mu}{\sigma})^2 = \sum_{i=1}^n(\frac{X_i - \bar X + \bar X - \mu}{\sigma})^2 \\= \sum_{i=1}^n(\frac{X_i - \bar X}{\sigma})^2 + n(\frac{\bar X - \mu}{\sigma})^2$$ 에서 표본분산 $S^2 = \sum_{i=1}^n(X_i - \bar X)^2/(n-1)$ 이므로 $$\sum_{i=1}^n(\frac{X_i - \mu}{\sigma})^2 = (\frac{(n-1)S^2}{\sigma^2}) + (\frac{\bar X - \mu}{\sigma/\sqrt{n}})^2$$ 여기서 $\sum_{i=1}^n(\frac{X_i - \mu}{\sigma})^2 \sim \chi^2(n)$ 이고, $(\frac{\bar X - \mu}{\sigma/\sqrt{n}})^2 \sim \chi^2(1)$ 이므로, 카이제곱분포의 가법성으로부터 $$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$$ 이 성립함을 짐작할 수 있습니다. <br> ### [ 분산이 동일한 두 정규모집단에서의 표본분산의 분포 ] 만약 주어진 랜덤표본들이 다음과 같다고 해봅시다. $$X_1, \cdots, X_{n} \text{이 서로 독립이고 } X_i \sim N(\mu_1, \sigma^2)(i=1,⋯,n)$$ $$Y_1, \cdots, Y_{n} \text{이 서로 독립이고 } Y_i \sim N(\mu_2, \sigma^2)(i=1,⋯,n)$$ 이 때 $$S_1^2 = \sum_{i=1}^{n_1}(X_i - \bar X)/(n_1-1), S_2^2 = \sum_{i=1}^{n_2}(Y_i - \bar Y)/(n_2-1)$$ 이라고 하면 $$\frac{(n_1-1)S_1^2}{\sigma^2} \sim \chi^2(n_1-1), \frac{(n_2-1)S_2^2}{\sigma^2} \sim \chi^2(n_2-1)$$ 이므로, 카이제곱분포의 가법성에 의해 $$\frac{(n_1-1)S_1^2 + (n_2-1)S_2^2}{\sigma^2} \sim \chi^2(n_1 + n_2 - 2)$$ 가 성립함을 알 수 있습니다. 이 때 $$S_p^2 = \frac{(n_1-1)S_1^2 + (n_2-1)S_2^2}{n_1+n_2-2}$$ 라고 정의한다면 위 사실을 아래와 같이 나타낼 수 있습니다. $$\frac{(n_1+n_2-2)S_p^2}{\sigma^2} \sim \chi^2(n_1 + n_2 - 2)$$ 여기서 정의한 $S_p^2$ 는 공통분산 $\sigma^2$ 의 추정량으로, 두 랜덤표본의 **합동표본분산(pooled sample variance)**이라고 합니다. [카이]: /posts/post-49 [티]: /posts/post-50 [엪]: /posts/post_51
$$$