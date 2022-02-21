# 이미지 비율 유지하기

## 깃블로그(Git Blog)의 경우&#x20;

포스팅에 사용되는 이미지는 `<img>` 태그를 사용하여 나타내고 있습니다.

* `<img>` 태그를 사용하면 이미지 크기를 쉽게 조정할 수 있습니다.&#x20;

그러나, 크기를 임의로 설정할 경우 화면 크기에 따라 이미지의 비율이 깨져버리는 경우가 종종 있습니다.

그럴 경우 다음과 같은 코드를 입력해주시면 됩니다.&#x20;

```css
img{
    object-fit: contain
}
```

## 깃북(Git Book)의 경우

깃북에서는 간단하게 /  &#x20;



![간단하게 다음 코드를 style태그나 css파일에 넣어주시면 됩니다.](https://w.namu.la/s/90620a3804cfebfaa23366c952bb1b879574094bb9b930bdfba13ec4f8a26244f3173af0b09baba5e2243c1b0d5b73741406412f3534a5bf8e9ab6d79d1e1b5272bd82195c8f7d12ae4baad45daf99e7b84a5236afbc2e8abf3fbd113b35df48)

```css
img{
    object-fit: contain
}
```
