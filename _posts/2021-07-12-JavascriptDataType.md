---
layout: single
title: "Javascript의 데이터 타입은 어떻게 나뉠까?"
description: "JS 데이터 타입이 나뉘게 되는 기준과 둘의 서로 다른 특징에 대해 알아봅니다."
tags: [JS]
comments: true
published: true
categories: JS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

자바스크립트에는 두 가지 데이터 타입이 존재합니다. 기본형과 참조형이죠.

- 기본형(primitive type) : number, string, boolean, null, undefined 등
- 참조형(reference type) : object, array, function, Date, RegExp 등

두 형식으로 나뉘고 일반적으로 기본형은 값을 할당 받고, 참조형은 값이 저장된 주소를 할당 받는다고 배웁니다. 그러나 엄밀히 말하면 이는 틀린 설명입니다. 이에 대해선 차차 서술하도록하겠습니다.

#### 1. 불변성과 가변성

기본형과 참조형 데이터의 차이는 불변성과 가변성을 통해 알아볼 수 있습니다. 주의해야 할 점은 이를 변수와 상수로 혼동하면 안된다는 것입니다. 변수와 상수를 구분짓는 변경 가능성은 변수 영역 즉, 식별자 영역에서 데이터 수정이 가능하냐로 나뉩니다. 여기서 말하는 수정 가능성은 데이터 자체가 아니라 그 변수가 가르키는 주소를 변경 가능하냐는 것이죠. 코드로 살펴보겠습니다.

```js
var a = 10; // 10에 대한 데이터 주소를 지칭
var b = { b: 11, c: 12 }; // {c: 11, e: 12}에 대한 위치를 지칭
```

이런 두 기본형, 참조형 데이터가 있다고 하죠. 둘은 서로의 변수 값에 대한 주소를 지정하고 있습니다. 이를 수정해 본다면.

```js
var a = 10; // 10에 대한 데이터 주소를 지칭
var b = { c: 11, e: 12 }; // {c: 11, e: 12}에 대한 위치를 지칭

a = 13;
b = { d: 14 };
```

위에서 볼 수 있듯 지칭하는 주소값이 변경되는 것을 볼 수 있습니다. 이제 13과 새로운 객체의 주소를 가지게 된 것이죠. 즉 기본형과 참조형은 모두 변수 영역에 대한 수정이 가능하며, 상수가 아닌 변수의 특징을 보이는 공통점이 있습니다.

둘이 차이를 보이는 부분은 불변성과 가변성입니다. 변수와 상수의 문제가 식별자 즉 변수 영역을 기준으로 판단된다면, 불변성과 가변성은 데이터 영역의 변경이 가능한지 여부에 따라 나뉩니다. 먼저 기본형을 살펴보겠습니다. 식별자가 지칭하는 주소값이 건물의 층이라고 예를 들겠습니다.

```js
var a = 10; // a는 10의 위치인 10층을 지칭
a = 13; // 주소가 수정되어 이제 13층을 지칭
a = 100; // 이제 100층을 지칭
```

보시듯 지정하는 주소 즉 층수가 계속 변경되는 것이 보입니다. 여기서 예시로 든 층수가 바로 데이터 영역입니다. 우리는 주소가 바뀔 뿐 층 자체의 데이터는 변하지 않는 것을 확인 할 수 있습니다. 즉, 지칭이 변할 뿐 10층에 10이 있고, 100층에 100이 있는 데이터 영역은 그대로인 것이죠. 이로써 기본형은 불병성을 가집니다.

이제 참조형 데이터를 살펴보죠.

```js
var b = { c: 11, e: 12 }; // {c: 11, e: 12}에 대한 위치를 지칭
b.c = 17; //c에 저장된 주소가 새로운 주소로 변경됨
```

변화의 차이가 보이시나요? 아마 지금은 뚜렷하게 보이진 않을 것입니다. 그러나 참조형은 기본형과 명백히 다릅니다. 기본형은 지칭하는 데이터 값이 다른 주소로 바뀌지만 그 내부의 값이 변하진 않았습니다. 참조형은 객체 내부의 c라는 데이터 위치는 그대로 입니다. 다만 그 내부에 c라는 값이 지정하던 주소가 11층에서 17층으로 변했죠. 즉 데이터 영역에서 수정이 이뤄진 것입니다! 이로써 참조형은 가변성을 지니는 것이죠. 개념이 조금 어렵기 때문에 둘의 차이가 발생하는 예시를 통해 자세히 알아보겠습니다.

#### 2. 예시를 통해 이해하기

```js
var a = 10;
var b = a;
var obj1 = { c: 10, d: "ddd" };
var obj2 = obj1;
```

먼저 기본형 데이터와 참조형 데이터를 선언합니다.

```js
var a = 10;
var b = a;
var obj1 = { c: 10, d: "ddd" };
var obj2 = obj1;

b = 15;
console.log(a, b); //10, 15가 출력
```

기본형 데이터는 데이터 복사 이후에 다른 변수를 할당해도 복사 대상이 변하지 않습니다. 즉 var b = a라는 선언에서 a는 10이 있는 위치인 10층으로 가라는 주소만 준 것이죠. 완전히 데이터를 복사한 것이 아닙니다. 이 때문에 a 값은 b 값이 변하더라도 영향을 받지 않습니다. 그러나 참조형 데이터는 다릅니다.

```js
var a = 10;
var b = a;
var obj1 = { c: 10, d: "ddd" };
var obj2 = obj1;

obj2.c = 20;
console.log(obj1, obj2); //같은 값을 출력
```

이 경우 놀랍게도 obj1, obj2는 같은 객체를 출력하게 됩니다. 어떤 일이 벌어진 것일까요? Obj2 = obj1으로 선언하는 순간에 참조형 데이터는 참조하는 데이터 값의 주소를 동일하게 할당합니다. 이를 건물 개념으로 설명하면.

```js
var a = 10;
var b = a;
var obj1 = { c: 10, d: "ddd" }; // 1번 건물로 가세요
var obj2 = obj1; //obj2도 1번 건물로 가세요

obj2.c = 20; //1번 건물이 변함
console.log(obj1, obj2); //둘 다 1번 건물을 참조하기 때문에 동일한 값이 출력됨
```

이렇게 건물이 동일하기 때문에 둘은 같아져 버리는 것입니다. 즉,

```
a !== b
obj1 === obj2
```

인 것이죠. 이것이 기본형 데이터와 참조형 데이터의 가장 큰 차이입니다. 만약 여기서 참조형 데이터가 서로 다른 값을 출력하도록 명령하고 싶다면 다른 건물로 할당을 변경해 줘야 합니다.

```js
var a = 10;
var b = a;
var obj1 = { c: 10, d: "ddd" }; // 1번 건물로 가세요
var obj2 = obj1; //obj2도 1번 건물로 가세요

obj2.c = { c: 14, d: "ddd" }; //2번 건물로 가세요
console.log(obj1, obj2); //둘의 건물이 다르기 때문에 서로 다른 값이 출력됨
```

재미있는 결과물이죠? 오늘은 이 정도로 마무리하고 계속해서 변수에 대해 깊게 들어가보도록 하겠습니다. 아 참 앞서서 기본형은 값을 할당 받고, 참조형은 값이 저장된 주소를 할당 받는다는 설명이 틀린 것이라고 했죠? 기본형과 참조형은 엄밀히 말하면 둘 다 주소를 참조하는 데이터라는 점은 JS에선 모든 데이터 타입이 결국 참조형이라 보아도 무방하기 때문입니다. 지금까지 설명했듯이 참조형 데이터의 경우에는 이러한 주소 참조 과정이 식별자 -> 건물 -> 층수로 3단계에 걸쳐 이뤄지고, 기본형은 식별자 -> 층수로 2단계 라는 부분만 다른 것이죠. 알아가면 알아갈 수록 재미있는 JS인 것 같네요. 다음에도 재미있는 이야기로 돌아오겠습니다 :)