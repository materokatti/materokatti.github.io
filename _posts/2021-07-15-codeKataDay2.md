---
layout: single
title: "CODEKATA Day 2 [JS] - Leetcode - 1108, 1, 7"
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

### 1. 1108 - Defanging an IP address

##### Given a valid (IPv4) IP `address`, return a defanged version of that IP address. A _defanged IP address_ replaces every period `"."` with `"[.]"`.

##### 예시 1

```
Input: address = "1.1.1.1"
Output: "1[.]1[.]1[.]1"
```

##### 예시 2

```
Input: address = "255.100.50.0"
Output: "255[.]100[.]50[.]0"
```

이번에도 난이도 easy의 문제로 예시만 보더라도 바로 파악이 되실거라고 생각됩니다. ip주소에서 .을 []로 대체하는 방법을 묻고 있습니다.

#### 내 답변

```js
var defangIPaddr = function (add) {
  let splitNums = add;
  let result = "";
  const arr = [];
  for (i = 0; i < splitNums.length; i++) {
    if (splitNums[i] === ".") {
      arr.push(i);
    }
  }
  return (
    splitNums.substring(0, arr[0]) +
    "[" +
    splitNums[arr[0]] +
    "]" +
    splitNums.substring(arr[0] + 1, arr[1]) +
    "[" +
    splitNums[arr[0]] +
    "]" +
    splitNums.substring(arr[1] + 1, arr[2]) +
    "[" +
    splitNums[arr[0]] +
    "]" +
    splitNums.substring(arr[2] + 1, arr[3])
  );
};
```

첫 답변은 굉장히 지저분했습니다. String.prototype.method를 이용하려고 고집하다가 대참사가 발생한 것이죠. 특히 return 값을 저렇게 길게 나열하면서 스스로 정말 나쁜 코드를 만들었구나.. 하면서 반성했습니다.

#### 보완 답변

```js
var defangIPaddr = function (add) {
  let ans = "";
  for (i = 0; i < add.length; i++) {
    console.log(add[i]);
    if (add[i] === ".") {
      ans += "[";
      ans += ".";
      ans += "]";
    } else {
      ans += add[i];
    }
  }
  return ans;
};
```

다른 언어로 푸신분의 답변을 보완 답변으로 재작성 해보았습니다. 복잡하게 문자열 메서드를 사용하기 보다, 단순하게 for 문으로 쓰는 것이 더 간결해 보입니다.

### 2. 1 - Two Sum

##### Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_. You may assume that each input would have **\*exactly\* one solution**, and you may not use the _same_ element twice. You can return the answer in any order.

##### 예시 1

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

##### 예시 2

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

##### 예시 3

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

#### 내 답변

```js
var twoSum = function (n, t) {
  const arr = n;
  const arrLength = arr.length;
  const target = t;
  const result = [];
  for (i = 0; i < arrLength; i++) {
    for (j = 0; j < arrLength; j++) {
      if (arr[i] + arr[j] === target && i !== j) {
        result.push(i);
      }
    }
  }
  return result;
};
```

#### 우수 답변

```js
const twoSum = (nums, target) => {
  const map = {};
  for (let i = 0; i < nums.length; i++) {
    const another = target - nums[i];
    if (another in map) {
      return [map[another], i];
    }
    map[nums[i]] = i;
  }
  return null;
};
```

### 3. 7 - Reverse Integer

##### Given a signed 32-bit integer `x`, return `x` _with its digits reversed_. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-231, 231 - 1]`, then return `0`.**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

##### 예시 1

```
Input: x = 123
Output: 321
```

##### 예시 2

```
Input: x = -123
Output: -321
```

##### 예시 3

```
Input: x = 120
Output: 21
```

##### 예시 4

```
Input: x = 0
Output: 0
```

#### 내 답변

```js
var reverse = function (x) {
  const absReverse = Math.abs(x).toString().split("").reverse().join("");
  if (absReverse > 2 ** 31) return 0;
  return absReverse * Math.sign(x);
};
```
