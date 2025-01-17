---
layout: single
title: "Javascript에서 variable은 어떻게 동작하는가?"
description: "JS variable의 동작을 자세히 알아봅니다."
tags: [JS]
comments: true
published: true
categories: JS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요 오늘 알아볼 주제는 Javascript를 배우면 가장 먼저 배우게 되는 variable 즉 변수입니다. 일반적으로 변수를 배우게 되면 선언에 대해서 배우게 되죠.

```js
var coding = "love";
let 비밀번호 = 486;
const IE = false;
```

상단의 예시처럼 가장 기본인 var 선언과 ES6 이후 등장한 let과 const 선언을 배우죠. 그러나 오늘은 변수에 대해 조금 더 깊게 들어가보려고 합니다. 단순히 선언하는 법이 아닌, 변수가 선언되면 컴퓨터에서 어떤 방식으로 데이터를 저장하고, 호출하며, 변경하는지 알아보겠습니다.

#### 1. 변수의 선언

변수의 선언은 간단히 하단과 같습니다.

```js
var a;
```

너무나 단순하죠. 이런 식으로 변수 없이 식별자(변수명)만 선언이 가능합니다. 마치 안에 아무것도 담지 않았지만(물론 undefined가 담기긴 했지만..) 그릇을 먼저 만들어 두는 개념이라고 보시면 됩니다.

```js
var a; // 식별자만 선언
a = 27; // 변수까지 선언
```

이제 변수까지 선언했습니다. 오늘의 목적은 이 단순하고 기본적인 작업을 컴퓨터가 어떻게 처리하는지 알아보는 것입니다. 자 여기까지 진행되면 사실상 변수의 선언이 마무리됩니다. 이제 어떤일이 일어나는지 살펴보죠.

#### 2. 선언된 식별자와 변수를 별도의 데이터로 저장

이제 선언된 식별자와 변수를 각각 다른 데이터 주소에 저장합니다. 이 점을 햇갈려하는 분들이 많은데요. 식별자가 변수와 동일하다고 해도(=) 둘은 다른 주소에 저장됩니다. 마치 데이터를 건물로 비유하자면 하단과 같이 저장되는 것이죠.

```js
var a; // 식별자는 1번방
a = 27; // 변수는 11번방
```

신기하죠? 왜 이런식으로 저장하는 것일까요? 바로 데이터를 효과적으로다르기 위함입니다. 변수와 식별자를 선언하는 시점에서는 동일한 것처럼 인지하지만 사실 둘의 데이터 형식, 변환 가능성은 전혀 다릅니다. 위의 예시의 경우 a라는 식별자는 문자열 형태의 데이터 타입이지만, 27인 변수는 숫자 형태의 데이터 타입에 저장됩니다. 둘은 서로 저장되는 방식이 다릅니다. 일례로 JS의 경우 숫자는 8바이트의 데이터 크기에 저장시키고 문자열은 그에 비해 더 유연합니다. 이러한 차이로 인해 둘이 동일한 위치에 저장되면 여러가지 혼선이 생기죠. 또한 식별자는 선언 후 변하지 않습니다. 그러나 변수는 변하죠. 계속 변하는 변수를 식별자와 동일한 위치에 저장하면 문제가 생길 수 밖에 없습니다. 때문에 이를 효과적으로 제어하려고 변수를 따로 저장해두는 겁니다.

#### 3. 만약 변수와 식별자를 한 공간에 저장하면?

만약 변수와 식별자가 한 공간에 저장되면 어떤 문제가 생길까요? 코드로 설명을 드리겠습니다.

```JS
var a = 27; // 1번방
var b = 33; // 2번방
var c = 77; // 3번방

b = 33333333; // 2번방에 저장 불가능, 과도하게 커진 데이터
```

위 상황이 이해가 되시나요? 즉 식별자와 변수를 일정한 위치에 저장해두면 변수가 과도하게 커져서 다른 공간을 침범할 경우 대처하기 어려워 집니다. 이 상황을 변수를 나눠 보겠습니다.

```js
var a; // 1번방
var b; // 2번방
var c; // 3번방

a = 27; // 4번방
b = 33; // 5번방
c = 77; // 6번방

b = 33333; // 7번방
```

이렇게 다른 위치에 저장해 버리면 됩니다. 물론 위의 경우처럼 순서대로 배정하는 것은 아닙니다만, 새로운 위치에 저장하는 개념은 동일합니다. 이렇게 되면 데이터의 재사용도 수월해집니다.

```js
var a; // 1번방
var b; // 2번방
var c; // 3번방

a = 27; // 4번방
b = 27; // 4번방
c = 27; // 4번방
```

이렇게 동일한 값을 변수로 지정하면 한 공간에서 데이터를 추출해올 수 있습니다. 훨씬 데이터 이용을 절약할 수 있습니다. 이렇듯 JS에서 변수의 활용은 최대한 컴퓨터의 데이터를 효과적으로 추출하고, 덜 이용하는 방향으로 시스템 되어있습니다. 이 글을 통해 변수에 대한 기본적인 이해가 깊어지는 시간이 되었길 바라면서 이만 물러갑니다 :)
