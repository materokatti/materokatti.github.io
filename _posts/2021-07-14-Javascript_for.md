---
layout: single
title: "CODEKATA Day 1 [JS] - Leetcode - 1927, 1920, 1480"
description: "Leetscode 1929, 1920, 1480번 문제풀이"
tags: [CODEKATA]
comments: true
published: true
categories: CODEKATA
typora-root-url: ../assets/images

sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요 오늘은 알고리즘 풀이 시간을 가져보려고 합니다.

### 1. 1927 - Concatenation of Array

문제는 Leetscode의 1929번 문항으로 두 행렬을 연결하는 문제입니다. 리츠코드에서 가장 정답률이 높을 정도로 쉬운 문제이죠. 함께 살펴보겠습니다.

##### 문제: 길이가 n인 정수 배열 nums가 인자로 주어졌다. 0 <= i < n일때, ans[i] == nums[i] 및 ans[i + n] == nums[i]인 길이 2n의 배열 ans를 생성하려고 합니다. 즉, ans는 두 개의 숫자 배열을 연결한 것입니다. 이 때 `ans` 를 반환(return)하시오.

##### 예시 1

```
Input: nums = [1,2,1]
Output: [1,2,1,1,2,1]
Explanation: The array ans is formed as follows:
- ans = [nums[0],nums[1],nums[2],nums[0],nums[1],nums[2]]
- ans = [1,2,1,1,2,1]
```

##### 예시 2

```
Input: nums = [1,3,2,1]
Output: [1,3,2,1,1,3,2,1]
Explanation: The array ans is formed as follows:
- ans = [nums[0],nums[1],nums[2],nums[3],nums[0],nums[1],nums[2],nums[3]]
- ans = [1,3,2,1,1,3,2,1]
```

#####

하단은 제가 문제에 대해 제출한 답변입니다.

#### 답변

```js
const addArray = (arr) => {
  const newArr = arr;
  const arrayLength = arr.length;

  for (let i = 0; i < arrayLength; i++) {
    newArr[i + arrayLength] = arr[i];
  }
  return newArr;
};
```

인자로 배열이 들어오는 함수 addArray를 선언합니다. 이후 새 배열을 선언하는데 기존 인자로 받아들인 요소들 넣어 일단 두 배열을 동일하게 만들어줍니다. 후에 arr 인자의 길이를 추출해 새로 생긴 newArr[i+행렬의 길이]를 더하는 for문을 통해 뒤에 차곡차곡 arr가 다시 쌓이도록 구조화했습니다.

#### 장애물

이 문제를 푸는데 상당한 시간이 걸렸는데, JS 함수에서 인자와 내부 반복문의 구조를 이해하지 못했기 때문입니다.

```js
const addArray = (arr) => {
  const newArr = arr;
  for (let i = 0; i < arr.lenght; i++) {
    newArr[i + arr.length] = arr[i];
  }
  return newArr;
};
```

하단이 제가 실수한 사례입니다. Array 길이를 변수로 선언해주지 않아 for문이 무한 루프에 걸려버렸습니다. 함수 외부에서 인자로 받아들이는 요소에 대해서는 변수 선언이 필요한지 체크를 해봐야 겠네요.

```js
const usingForIn = (arr) => {
  const newArr = arr;
  const arrayLength = arr.length;
  for (let i in arr) {
    newArr[+i + arrayLength] = arr[i];
  }
  return newArr;
};
```

위 사례처럼 for in 문으로도 변경해 간결하게 풀 수 도 있습니다. 그러나 사실 가장 쉬운 방법은 concat 메서드를 사용하는 것이죠.

```js
let getConcatenation = function (nums) {
  const ans = nums.concat(nums);
  return ans;
};
```

concat을 사용하면 뒤의 배열을 끊김없이 바로 연결해주기 때문에 가장 간결한 코드로 쉽게 해결할 수 있습니다.

### 2. 1920 - Build Array from Permutation

##### 문제: 0부터 시작하는 배열 nums가 주어진다. 각 0 <= i < nums.length에 대해 ans[i] = nums[nums[i]]인 동일한 길이의 배열 ans를 만들고 반환한다.

##### 예시 1

```
Input: nums = [0,2,1,5,3,4]
Output: [0,1,2,4,5,3]
Explanation: The array ans is built as follows:
ans = [nums[nums[0]], nums[nums[1]], nums[nums[2]], nums[nums[3]], nums[nums[4]], nums[nums[5]]]
    = [nums[0], nums[2], nums[1], nums[5], nums[3], nums[4]]
    = [0,1,2,4,5,3]
```

##### 예시 2

```
Input: nums = [5,0,1,2,3,4]
Output: [4,5,0,1,2,3]
Explanation: The array ans is built as follows:
ans = [nums[nums[0]], nums[nums[1]], nums[nums[2]], nums[nums[3]], nums[nums[4]], nums[nums[5]]]
    = [nums[5], nums[0], nums[1], nums[2], nums[3], nums[4]]
    = [4,5,0,1,2,3]
```

주어진 배열 nums에 대해, 새 배열 ans로 전환해 주는 문제입니다. 전환 구조는 ans[i] = nums[nums[i]]을 따르면 됩니다. 구조가 햇갈려보이지만 ans = [nums[nums[0]], nums[nums[1]], nums[nums[2]], nums[nums[3]], nums[nums[4]], nums[nums[5]]] 형식을 따른다는 문제 설명을 통해 이해하면 어렵지 않습니다.

#### 답변

```js
var buildArray = function (nums) {
  const ans = [];
  const arrLength = nums.length;
  for (let i = 0; i < nums.length; i++) {
    ans.push(nums[nums[i]]);
  }
  return ans;
};
```

이번 문제는 매우 쉽게 풀렸습니다. 역시 for문을 사용했는데요. ans라는 새로운 배열을 선언했구요. nums의 길이를 변수로 선언해주는 것을 통해 이전의 실수를 되풀이하지 않았습니다. for문은 단순합니다. 배열을 길이대로 반복하되 push 메서드를 통해서 뒤에 nums[nums[i]]구조로 배열을 순서대로 붙여줬습니다.

### 3. 1480 - Running Sum of 1d Array

##### 문제

Given an array `nums`. We define a running sum of an array as `runningSum[i] = sum(nums[0]…nums[i])`.

Return the running sum of `nums`.

##### 예시 1

```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```

##### 예시 2

```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```

단순한 문제입니다. 주어진 배열의 다음 요소는 그때까지 배열 요소의 Sum 값을 표현한 배열을 선언하는 것입니다. 배열의 길이도 동일하기 때문에 어려운 문제는 아니죠.

#### 답변

```js
var runningSum = function (nums) {
  const sumArr = [];
  const inputArr = nums;
  const lengthArr = nums.length;
  for (i = 0; i < lengthArr; i++) {
    let miniSum = 0;
    for (j = 0; j < i + 1; j++) {
      miniSum = miniSum + inputArr[j];
      sumArr[i] = miniSum;
    }
  }
  return sumArr;
};
```

오래 걸리진 않았지만, 답변이 썩 마음에 들지는 않습니다. 보다 더 효과적인 코드가 있을것이라 생각되지만 오늘은 for 반복문 뿐 떠오르지 않네요 ㅜㅜ. 구조는 지금까지와 동일합니다. 다만 이중 for문이 선언되었다는 점이 이전 문제들과 차이를 보입니다. 배열 4자리를 선언하고 각 자리마다 sum을 해줘야 하기 때문에 반복문이 2번 나타나는 것이죠. 참, 반복문 값을 저장할 변수로 miniSum을 선언했습니다. 처음에 아무 생각 없이 내부 for문 안에서 선언해서 덧셈이 되지 않아 잠깐 당황하기도 했네요 ㅎㅎ. 아무튼 이중 for문 구조로 이번 문제도 어찌저찌 넘어가게 되었습니다.
