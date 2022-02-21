# 모평균에 관한 추론

#### 모평균의 신뢰구간

1. 모표준편차 $$\sigma$$가 기지인 경우,

* 표준화된 표본평균에 대하여 $$\frac{\bar X - \mu}{\sigma / \sqrt n} \sim N(0, 1)$$임을 이용하여 $$\mu$$에 관한 추론을 할 수 있습니다.

1. 모표준편차 $$\sigma$$가 미지인 경우,

* $$\sigma$$ 대신 그 추정량인 $$S$$를 사용합니다. (스튜던트화)&#x20;

$$
\frac{\bar X - \mu}{S / \sqrt n} \sim t(n-1)
$$

이러한 표본분포로부터

$$P\{-t_{\alpha/2}(n-1) \leqq \frac{\bar X - \mu}{S / \sqrt n} \leqq t_{\alpha/2}(n-1)\} = 1 - \alpha$$

즉,

$$P\{\bar X - t_{\alpha/2}(n-1) S / \sqrt n \leqq \mu \leqq \bar X + t_{\alpha/2}(n-1) S / \sqrt n\} = 1 - \alpha$$

따라서 모평균 $$\mu$$에 대한 $$100(1-\alpha)%$$ 신뢰구간을 다음과 같이 구할 수 있습니다.

$$(\bar x - t_{\alpha/2}(n-1) s / \sqrt n, \bar x + t_{\alpha/2}(n-1) s / \sqrt n)$$

#### t-test ~~(어디선가 들어봤을 그 이름)~~

스튜던트화된 표본평균을 이용한 모평균의 유의성 검증을 t검정 혹은 t-test라고 합니다.

귀무가설이 $$H_0 : \mu = \mu_0$$인 경우에 **검정통계량**은

$$T = \frac{\bar X - \mu_0}{S / \sqrt n}$$

이고, 이의 관측값을 $$t$$라고 할 때, 다음이 성립합니다.

|                        |                    유의확률                    |              유의수준 alpha의 기각역              |
| :--------------------: | :----------------------------------------: | :---------------------------------------: |
|  $$H_1:\mu \gt \mu_0$$ |             $$P=P(T \geqq t)$$             |         $$t \geqq t_\alpha (n-1)$$        |
|  $$H_1:\mu \lt \mu_0$$ |             $$P=P(T \leqq t)$$             |        $$t \leqq - t_\alpha (n-1)$$       |
| $$H_1:\mu \neq \mu_0$$ | $$P=P(\vert T \vert \geqq \vert t \vert)$$ | $$\vert t \vert \geqq t_{\alpha/2}(n-1)$$ |

만약 유의확률 $$P$$가 유의수준 $$\alpha$$보다 작다면, 충분히 유의하다고 할 수 있다.

✔ 유의하다 = 귀무가설 $$H_0$$을 기각하기에 충분하다.

### 참조

* 일반통계학(영지문화사) 서적
