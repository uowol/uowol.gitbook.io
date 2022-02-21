# Iris 데이터 분석

### Iris

R에서 기본으로 제공하는 데이터로, Setosa, Versicolor, Virginica 이 세가지 종류의 붓꽃에 대한 데이터가 각각 50개씩, 총 150개의 데이터를 제공합니다.

### 2021.02.05.

{: class='date' id='date1'}

#### \[ R에서 iris 데이터를 사용하는 방법 ]

```
data = iris
head(data)
```

&#x20;{:style="text-align:center;"}

`head()` 함수를 사용하여 처음 6개의 데이터만 꺼내본 상황입니다.

더 자세한 정보를 알기 위해 `str()` 함수로 감싸주면

```r
str(data)
'data.frame':	150 obs. of  5 variables:
 $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
 $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
 $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
 $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
 $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...
```

iris 데이터의 형태는 data.frame으로, R에서 list를 기반으로 만든 object입니다.

data.frame은 각 수준에 접근하기가 용이한데, data$Sepal.Length 와 같이 변수에 $ 를 붙이는 방식으로 접근할 수 있습니다.

```r
str(data$Sepal.Length)
 num [1:150] 5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
```

그러면 이렇게 num 형태의 벡터를 리턴받을 수 있습니다.

\


#### \[ 데이터 시각화 ]

이번엔 데이터를 시각화하여 어떤 패턴이 드러나는지 확인해보겠습니다.

```r
par(mfrow=c(2,2))
plot(data$Sepal.Length, col=data$Species)
plot(data$Sepal.Width, col=data$Species)
plot(data$Petal.Length, col=data$Species)
plot(data$Petal.Width, col=data$Species)
```

&#x20;{:style="text-align:center;"}

`par(mfrow=c(2,2))`는 화면을 2\*2로 나누어 위에 둘 아래 둘 이렇게 시각화하라는 함수입니다.

종에 따른 차이를 알아보기 위해 꽃의 종류에 따라 색깔을 다르게 표현해보았습니다.

시각화된 데이터를 통해 꽃의 종류에 따라 꽃받침sepal과 꽃잎petal의 크기가 유의미한 차이가 있다는 것을 확인할 수 있었습니다.

위 그래프의 x축은 단순히 데이터의 순서로, 데이터가 꽃의 종류에 따라 정렬되어 있을 뿐이지 y축과의 연관관계라고 할 것이 없습니다.

하지만 꽃의 종류에 따른 유의미한 차이가 있다는 것을 알아냈으므로, 그것을 x축의 기준으로 두어 조금 더 가공된 그래프를 그려보겠습니다.

```r
par(mfrow=c(2,2))
plot(data$Sepal.Length~data$Species)
plot(data$Sepal.Width~data$Species)
plot(data$Petal.Length~data$Species)
plot(data$Petal.Width~data$Species)
```

&#x20;{:style="text-align:center;"}

위 그래프에 대한 설명은 아래와 같습니다.

![그림4](https://naysan.ca/wp-content/uploads/2020/06/box\_plot\_ref\_needed.png)\
출처: https://towardsdatascience.com/understanding-boxplots-5e2df7bcbd51 {:style="text-align:center;"}

\


#### \[ 평균값과 중앙값 비교 ]

평균값은 **(데이터의 합)/(데이터의 개수)** 이고 중앙값은 말 그대로 **데이터를 정렬했을 때 가운데에 있는 수**를 의미합니다.

만약 평균값과 중앙값 사이에 유의미한 차이가 있다면 그 데이터는 어느 한 쪽으로 편향된 데이터라고 추측할 수 있습니다.

![그림5](https://img1.daumcdn.net/thumb/R1280x0.fpng/?fname=http://t1.daumcdn.net/brunch/service/user/2Rsf/image/fvBoygDWyEluU0Wk7nl61DzhPbo.png)\
출처: https://www.quora.com/How-is-the-gender-pay-gap-calculated-in-the-US {:style="text-align:center;"}

```r
# 꽃 종류에 따라 데이터를 분류
data.setosa = data[data$Species == "setosa",]
data.versicolor = data[data$Species == "versicolor",]
data.virginica = data[data$Species == "virginica",]

# head(data.setosa)
# typeof(data.setosa) # list, data.frame은 list에 기반한 object이므로 lapply 사용가능

data.setosa.mean = lapply(data.setosa[, 1:4], mean)
data.setosa.median = lapply(data.setosa[, 1:4], median)

title = names(data.setosa.median)

print(" = Setosa ====")
paste("중앙값", title, data.setosa.median)
paste("평균", title, data.setosa.mean)

data.versicolor.mean = lapply(data.versicolor[, 1:4], mean)
data.versicolor.median = lapply(data.versicolor[, 1:4], median)

print(" = Versicolor ====")
paste("중앙값", title, data.versicolor.median)
paste("평균", title, data.versicolor.mean)

data.virginica.mean = lapply(data.virginica[, 1:4], mean)
data.virginica.median = lapply(data.virginica[, 1:4], median)

print(" = Virginica ====")
paste("중앙값", title, data.virginica.median)
paste("평균", title, data.virginica.mean)
```

\
결과값 {:style="text-align:center;"}

위 데이터의 평균값과 중앙값 사이에는 큰 차이가 없으므로 절사 등의 조치를 취할 필요가 없을 것 같습니다.

***

### 2021.02.18.

{: id='date2' class='date'}

#### \[ 모평균의 추정 ]

🎈 모평균 추정을 하기 이전에, 다음 포스팅에서 **통계적 추론**에 대한 개념을 숙지하고 오는 것을 권해드립니다.

🎈 스튜던트화에 대한 개념을 다음 포스팅에서 읽고 오는 것을 권해드립니다.

모평균 $\mu$ 를 추정하기 위한 방법으로 표본평균 $\bar X$ 를 사용하거나 중앙값을 사용하곤 하는데, 이번에 다룰 방법은 표본평균 $\bar X$ 를 이용하는 방법입니다.

표본평균의 분포를 본격적으로 다루기 이전에 모집단의 분포가 정규분포인지를 먼저 따져보아야합니다.

물론 무한모집단에서의 표본평균의 분포는 표본의 크기가 충분히 크다면 **중심극한정리**를 통해 정규분포를 따른다는 것을 알고 있지만, 확실하게 따지고 가는 것이 좋겠죠?

\


#### \[ 정규분포 분위수대조도(Q-Q plot) ]

1.  Setosa의 경우


2.  Versicolor의 경우


3.  Versicolor 경우



{:style="text-align:start;"}

Setosa의 Width 데이터가 조금 모호하긴 하지만 대체적으로 모든 데이터의 분위수대조도가 직선을 이루고 있는 것을 확인했습니다.

따라서, 모집단의 데이터 역시 정규분포를 따르고 있다는 긍정적인 추측을 할 수 있습니다.

\


#### \[ 모집단의 신뢰구간 ($\sigma$ 가 기지(旣知)일때) ]

모집단의 신뢰구간을 구하기 위해선 어떤 계산을 해야할까요?

확률변수 $X\_1, \cdots, X\_n$ 이 정규분포 $N(\mu, \sigma^2)$의 랜덤표본일 때

$$\frac{\bar X - \mu}{\sigma/\sqrt{n}} \sim N(0, 1)$$

이고, 표준정규분포의 $(1-\alpha)$ 분위수는

$$P\{\frac{\bar X - \mu}{\sigma/\sqrt{n}} \ge z_\alpha\} = \alpha$$

$$P\{\frac{\bar X - \mu}{\sigma/\sqrt{n}} \le z_\alpha\} = 1 - \alpha$$

임을 이용하여 아래와 같이 $100(1-\alpha)$ % 신뢰구간을 구할 수 있습니다.

표준정규분포는 0을 기준으로 대칭이므로,

$$P\{\vert \frac{\bar X - \mu}{\sigma/\sqrt{n}} \vert \le z_{\alpha/2}\} = 1 - \alpha$$

따라서,

$$P\{\bar X - z_{\alpha/2}\cdot\sigma/\sqrt{n} \le \mu \le \bar X + z_{\alpha/2}\cdot\sigma/\sqrt{n}\} = 1-\alpha$$

이와같이 신뢰구간(C.I)을 구할 수 있습니다.

$$\mu \in (\bar X - z_{\alpha/2}\cdot\sigma/\sqrt{n}, \bar X + z_{\alpha/2}\cdot\sigma/\sqrt{n}), \quad \text{100(1-α)% C.I}$$

\


#### \[ 모집단의 신뢰구간 ($\sigma$ 가 미지(未知)일때) ]

하지만 대부분의 경우 우리는 $\sigma$ 를 알지 못합니다. 이럴 경우 $\sigma$ 대신 표본표준편차 $S$ 를 사용하는 스튜던트화(Studentization) 를 하게 됩니다.

```
오늘은 여까지!
```
