# Q-Learning 강화학습

### 예제

다음은 Q-Learning을 활용해 구현해본 길찾기 어플리케이션입니다. 이번 포스팅에서는 Q-Learning에 대해 간략히 설명하고 아래 어플리케이션을 만들어보면서 활용하는 방법을 익혀보겠습니다.

사용방법

1. init
   * 빈 칸을 1번 클릭하면 '벽', 2번 클릭하면 '함정', 3번 클릭하면 '도착지', 4번 클릭하면 '빈 공간'이 만들어집니다.
   * 빈 칸을 오른쪽 클릭하면 '출발지'로 설정할 수 있습니다.
   * 도착지와 출발지는 하나씩만 존재할 수 있습니다.
2. learn
   * \[학습 시작하기] 버튼을 누르면 마우스 이벤트 대신 키보드 이벤트를 받기 시작합니다.
   * 상/하/좌/우 키로 파란 블럭을 움직일 수 있으며 '도착지' 또는 '함정'에 빠지면 다시 처음 위치로 돌아옵니다.
   * 학습이 완료되었다는 상태메시지가 뜨기 전까지 계속하여 블럭을 도착지까지 옮겨줍니다.
3. start
   * 학습이 완료되었다면 \[학습 결과 확인하기] 버튼을 눌러 결과를 확인할 수 있습니다.

{% embed url="https://codepen.io/uOwOn/pen/abVGZKj" %}
click the 0.5x button on the bottom.
{% endembed %}

### 개념

#### \[ Model-Free Algorithm ]

기존의 Model-Based Algorithm은 **Environment(환경)에 대해 알고 있으며 우리의 행동에 따른 환경의 변화를 알고 있습니다.**

그에 반해 Model-Free Algorithm은 **Environment(환경)에 대해 알지 못하고 Action에 따른 Next State와 Next Reward를 '수동적으로' 얻게 됩니다.** 조금 더 자세히 이야기해보면, Model-Free Algorithm의 Agent가 Action을 취하면 Environment는 그에 대한 Reward(보상)과 State를 반환합니다.

이 알고리즘은 환경이 어떻게 동작하는지 모르기때문에 Exploration(탐사) 즉, 실제로 부딪혀가며 **Trail and Error를 반복해 Policy Function을 점차 학습**시켜야 합니다.

![그림1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqTURh%2FbtqBOsVDNcz%2FH9KgbAldN1olQjXbEKa7Bk%2Fimg.png)\
그림출처: [망나니개발자](https://mangkyu.tistory.com/61?category=767742) {: style='text-align:center;'}

\


#### \[ Q-Learning ]

Q-Learning은 **Model 없이(Model-Free) 학습하는 강화학습 알고리즘** 즉, Environment(환경)에 대해 알지 못하고 Action(활동)에 따른 결과(Next State, Next Reward)를 받아 Exploration(탐험)을 통해 점차 학습시키는 알고리즘입니다.

Q-Learning의 목표는 유한한 마르코프 결정 과정(FMDP)에서 **Agent가 특정 상황에서 특정 행동을 하라는 최적의 Policy를 배우는 것**으로, 현재 상태로부터 시작하여 모든 연속적인 단계들을 거쳤을 때 전체 보상의 예측값을 극대화시킵니다.

이는 한 상태에서 다른 상태로의 전이가 확률적으로 일어나거나 보상이 확률적으로 주어지는 환경에서도 별다른 변형 없이 적용될 수 있습니다.

\


#### \[ Q-Value ]

Q-Learning에서는 어떤 State S에서 어떤 Action A를 했을 때, 그 행동이 가지는 Value를 계산하는 Q-Value를 사용하는데, 이를 행동-가치 함수라고도 부릅니다.

여기서 'Q'는 현재 상태에서 취한 행동의 보상에 대한 quality를 상징합니다.

이러한 행동-가치 함수는 Discount Factor(할인계수)를 사용하여 특정 Action을 취했을 때, Episode가 종료되기까지 reward의 총합의 예측값을 계산합니다.

현재 상태로부터 $Δt$ 시간이 흐른 후에 얻는 보상 $r$은 $γ^{Δt}$ 만큼 할인되어 $r∗γ^{Δt}$로 계산되는데 여기서 $γ$ 는 0\~1사이의 값을 갖는 Discount Factor로 현재 얻는 보상이 미래에 얻는 보상보다 얼마나 더 중요한지를 의미합니다.

\


#### \[ Q-Learning Algorithm ]

알고리즘이 시작되기 전에 Q 함수는 고정된 임의의 값을 갖습니다. 그리고 매 time-step($t$)마다 Agent는 행동 $a\_t$를 선택하고 보상 $r\_t$를 받으며 새로운 상태 $s\_{t+1}$로 전이하고 Q값을 갱신합니다.

이것을 수식으로 나타내면 아래와 같습니다.

$$Q(s_t,a_t)←(1−α)⋅\underbrace{Q(s_t,a_t)}_{\text{old value}}+\underbrace{α}_{\text{learning rate}}⋅\left(\overbrace{\underbrace{r_t}_{\text{reward}}+\underbrace{γ}_{\text{discount factor}}⋅\underbrace{\max_aQ(s_{t+1}, a)}_{\text{estimate of optimal future value}}}^{\text{learned value}}\right)$$

***

### 예제 실습

#### 0. Platform

* HTML, JavaScript

\


#### 1. UI 제작

작성한 프로그램을 화면에 출력하기 위해선 UI를 만들어주어야 합니다. 저는 HTML과 CSS를 사용해 화면을 구성하고 JavaScript를 적용하여 사용자의 이벤트에 반응할 수 있도록 구현해주었습니다.

이 때, 화면에 격자나 기타 도형들을 그리기 위해 `<canvas>` tag를 사용했습니다.

UI는 간단하고 직관적입니다. N\*M 크기의 격자가 주어지고 클릭 이벤트에 반응하여 벽이나 함정, 또는 출발지와 도착지, 즉 환경(Environment)을 직접 구성할 수 있게 하였습니다.

또한, 이후 Learn 단계에서 키보드 이벤트에 반응하여 Action과 그에 따른 Q-value의 업데이트가 일어나도록 만들었습니다.

&#x20;{: style="text-align:center"}

* 회색 타일 : 벽 => 진행할 수 없습니다.
* 파랑색 타일 : 출발지 => 출발지입니다.
* 빨강색 타일 : 함정 => reward로 -1 을 반환합니다.
* 초록색 타일 : 도착지 => reward로 +1 을 반환합니다.

\


#### 2. Step

해당 프로그램은 크게 세 단계로 작동합니다.

1. **환경(Environment) 구축하기**
   * 클릭 이벤트에 따라 빈 칸에 벽, 함정, 출발지, 도착지를 생성할 수 있습니다.
   * 이 때, 출발지와 도착지는 개수가 하나로 고정되어 있습니다.
   * 또한, 이 때 키보드 이벤트는 처리하지 않습니다.\
     \

2. 직접 **개체를 움직여(Action) 학습시키기(Q-value Update)**
   * 방향키에 따라 파란색 개체(Entity)를 이동시킬 수 있습니다.
   * 개체는 출발지에서부터 움직입니다.
   * 이 때, 마우스 이벤트는 처리하지 않습니다.\
     \

3. 학습이 끝나면 **결과 확인하기**
   * 학습이 완료되면 해당 메시지가 출력됩니다.
   * 확인하기 버튼을 눌러 학습된 움직임을 확인할 수 있습니다.

\


#### 3. Q-Learning

이제 환경(Environment)이 주어졌을 때, 개체의 Action에 따라 Q-value가 어떻게 업데이트되는지에 대해, 즉, 학습 과정에 대해 알아보겠습니다.

모든 칸에는 \[ 상, 하, 좌, 우 ] 각각에 대한 Q-value가 들어있고, 초기의 Q-value는 모두 0으로 설정해주었습니다.

사용자가 \[ 상, 하, 좌, 우 ] 중 하나를 선택하여 이동(Action)하면 해당 Action에 대한 Q-value를 아래 공식을 사용하여 업데이트시켜줍니다.

$$Q(s_t,a_t)←(1−α)⋅\underbrace{Q(s_t,a_t)}_{\text{old value}}+\underbrace{α}_{\text{learning rate}}⋅\left(\overbrace{\underbrace{r_t}_{\text{reward}}+\underbrace{γ}_{\text{discount factor}}⋅\underbrace{\max_aQ(s_{t+1}, a)}_{\text{estimate of optimal future value}}}^{\text{learned value}}\right)$$

Reward는 개체의 Action에 따라 결정되는데, Action에 따른 결과가 함정(RED)이라면 Reward는 -1이 되고 'Dead' State를 갖습니다. 반대로 Action에 따른 결과가 도착지(GREEN)이라면 Reward는 +1이 되고 'Arrive' State를 갖습니다.

이 때, State가 'Dead' 또는 'Arrive'라면 개체는 다시 출발지로 이동합니다.

그리고 만약 Action의 결과가 빈 칸이라면 Reward는 0이 되고 Action의 방향이 벽으로 막혀있다면 해당 Action을 진행하지 않습니다.

이와 같이 학습을 진행한다면, 함정이나 빈 칸은 $\max\_aQ(s\_{t+1}, a)$에 별다른 영향을 미치지 못하기 때문에 도착지(Reward=+1)의 방향으로 학습이 진행될 것 입니다.

학습이 정상적으로 진행되었을 때 각 칸의 Q-value는 아래 그림과 같습니다.

&#x20;{: style="text-align:center"}

1. 첫 번째 학습
   * \[ 상, 상 ] : (2, 3) 위치의 \[ 상 ] Q-value를 +1로 업데이트 합니다.
2. 두 번째 학습
   * \[ 상, 상 ] : (3, 3) 위치의 \[ 상 ] Q-value를 +0.9로 업데이트 합니다. (discount factor의 값을 0.9로 설정했습니다.)
   * 사실상 **학습은 여기서 완료**되었다고 할 수 있습니다.
3. 세 번째 \~ n번째 학습
   * 개체가 함정에 빠질 수 있는 경우는 (2, 1) 위치에서 \[ 상 ]으로 움직였을 때 뿐입니다. 이 경우 (2, 1) 위치의 \[ 상 ] Q-value를 -1로 업데이트 합니다.
   * $\alpha$(Learning Rate) 값을 1로 설정해 두었기 때문에 더 이상의 변화는 일어나지 않습니다.

\


#### 결과 확인하기

위의 [예제](broken-reference)를 통해 학습 결과를 확인하실 수 있습니다.

\*{ box-sizing: border-box; } .container{ position: relative; } canvas{ position: absolute; border: 1px solid #2e2e2e; }
