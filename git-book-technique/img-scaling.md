---
title: '이미지 비율 유지하기'
description: '잠시 짬을 내서 유지보수!'
date: 2020-11-17 19:03:34 +0900
categories: Modify_Settings
---
# 이미지 비율 유지하기

## 마크다운(Mark Down)의 경우

이미지를 포스팅할 때 `<img>` 태그를 사용하는데 모바일과 같이 작은 화면에서 볼 경우 이미지가 잘리는 일이 발생하곤 합니다. 그럴 경우, 간단하게 다음 코드를 `style`태그나 `css`파일에 넣어주시면 됩니다.

```css
img{ object-fit: contain } 
```

## 브라우저(gitbook.io)의 경우

간단하게  `Ctrl`+`/` 을 누르고 `Insert Images`를 선택, 그리고 URL에 이미지 주소를 붙여 넣어주면 됩니다.