---
layout: single
title: "CODEKATA Day 6 [JS] - Leetcode 169번 문제풀이"
description: "Leetscode 169번 문제풀이"
tags: [CODEKATA]
comments: true
published: true
categories: CODEKATA
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

오늘 푼 문제는 개인적으로 엄밀하게 설정되지 못한 것 같은 아쉬움이 있습니다. 문제의 조건을 조금 더 구체적으로 정해주면 더 좋지 않았을까 하는 아쉬움이 있었지만, 그럼에도 그런 엄밀함을 포함한 정답은 찾아내지 못해 아쉬웠습니다.

### LeetCode 169. Majority Element

##### 문제

```markdown
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.
```

##### 예시 1

```
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

##### 예시 2

```
Input: nums = [3,2,3]
Output: 3
```

#### 내 답변

```js
var majorityElement = function (nums) {
  nums.sort((a, b) => a - b);
  return nums[Math.floor(nums.length / 2)];
};
```

처음 구한 답변은 엄격하지 못한 해답이라고 생각하는데요. 답이 통과가 되어 무안하기도 합니다. 문제에서 배열 속의 숫자의 종류가 2개라는 것을 언급하지 않았고, 또한 배열이 홀수가 된다는 말도 없습니다. 그러나 제 답변은 배열을 크기 순으로 정렬하고 그 배열의 중간 값을 구하는 방식입니다. 만약 숫자가 3종류가 나오거나 두 가지라도 동일한 경우 즉, 짝수의 배열일 경우 정답을 도출하지 못합니다.

#### 우수 답변

```js
var majorityElement = function (nums) {
  var obj = {};

  for (var i = 0; i < nums.length; i++) {
    obj[nums[i]] = obj[nums[i]] + 1 || 1;
    if (obj[nums[i]] > nums.length / 2) {
      return nums[i];
    }
  }
};
```

javascript의 추천 답변 중에 가장 마음에 들었던 답변입니다. 객체를 선언해서 각 숫자를 객체에 더해나가 결과적으로는 내부 숫자를 키 값으로 하고 개수를 value로 하는 객체가 완성됩니다. 좀 더 길더라도 이 답변이 마음에 든 이유는 앞서 말한 여러가지 변수도 통제가 되기 때문입니다. 숫자의 종류를 다양화해도 객체에 일일이 저장해주기 때문에 구별이 가능하고, 심지어 가장 우세한 숫자가 없는 경우 역시 출력이 가능합니다. 여러모로 가장 마음에 드는 답변이 아닌가 싶네요.
