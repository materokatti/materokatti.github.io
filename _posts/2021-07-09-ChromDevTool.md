---
layout: single
title: "Javascript array.map()과 array.forEach() 메서드"
description: "Javascript array.map()과 array.forEach() 메서드"
tags: [JS]
comments: true
published: true
categories: JS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

오늘은 자바스크립트에서 정말 많이 활용되는 두 메서드, array.map( )과 array.forEach에 대해 이해하는 시간을 가져보겠습니다. 배열에 반복 작업을 하거나 각각의 요소에 수정이 필요할 때 등등 다양한 상황에서 활용되는 기능입니다. 그 때문에 정말 많이 쓰이는 함수이죠.

#### 1. Array.map()

Map 메서드는 배열의 각각 요소들에 반복 작업을 하고 새로운 배열로 수정하는 일을 합니다. 매우 단순하고 간결한 일입니다. 그러나 너무나 효과적이고 꼭 필요한 일이기 때문에 자주 사용하는 소중한 메서드입니다. 예시를 보겠습니다.

```js
const originalArray = [1, 2, 3, 4, 5];

const newArray = originalArray.map(
  (addOne = (number) => {
    return number + 1;
  })
);

console.log(originalArray); // [ 1, 2, 3, 4, 5 ]
console.log(newArray); // [ 2, 3, 4, 5, 6 ]
```

각 배열의 요소에 1씩 수를 더하는 addOne 함수를 적용하는 map 메서드 입니다. 굉장히 효과적이죠? Arrow 함수를 콜백 함수로 사용했지만 굳이 이렇게 복잡하게 할 필요는 없습니다.

```js
const originalArray = [1, 2, 3, 4, 5];

const newArray = originalArray.map((number) => number + 1);

console.log(originalArray); // [ 1, 2, 3, 4, 5 ]
console.log(newArray); // [ 2, 3, 4, 5, 6 ]
```

자! 이렇게 하면 한결 간결해졌습니다. 함수를 익명으로 선언하고, 인자 위치는 인자가 하나일 경우 괄호 생략이 가능합니다. 또 return만 존재하는 함수의 경우 굳이 return을 쓰지 않아도 된다는 arrow 함수의 기능을 활용하면 이렇게 간결하고 가독성이 뛰어난 코드를 작성할 수 있습니다.

#### 2. Arrow.forEach()

forEach 메서드는 for 대신 활용하는 반복문입니다. map과 다른 점은 forEach 함수 자체는 return 하는 것이 없다는 것이죠. return은 오히려 for 반복문의 탈출 용도로 쓰입니다. 즉 map 함수가 수정된 배열을 return 한다면, forEach는 반복 작업 뿐 return하는 값은 없는 것이죠.

```js
let startWithNames = [];
let names = ["a", "ab", "cbb", "ada"];

names.forEach((el) => {
  if (el.startsWith("a")) {
    startWithNames.push(el);
  }
});

console.log(startWithNames); //[ 'a', 'ab', 'ada' ]
```

위의 상황처럼 모든 함수에 반복 작업을 적용하는 경우에도 사용하구요.

```js
let startWithNames = [];
let namesIndex = [];
let names = ["a", "ab", "cbb", "ada"];

names.forEach((el, idx) => {
  if (el.startsWith("a")) {
    startWithNames.push(el);
    namesIndex.push(idx);
    return;
  }
});

console.log(startWithNames); //[ 'a', 'ab', 'ada' ]
console.log(namesIndex); // [ 0, 1, 3 ]
```

이렇게 두번째 인자를 주면 요소의 index 값을 지정하는데 이를 유용하게 활용할 수도 있습니다. 가정문과 함께 일정한 조건을 만족하는 요소만 추출하고 그 요소들의 위치를 알아내야 하는 경우 상당히 유용하게 쓰일 수 있습니다.
