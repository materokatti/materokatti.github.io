---
layout: single
title: "CODEKATA Day 7 [JS] - Leetcode 14번 문제풀이"
description: "Leetscode 3번 문제풀이"
tags: [CODEKATA]
comments: true
published: true
categories: CODEKATA
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

오늘 문제는 2가지 인자를 받는데요. 첫 인자는 숫자 배열, 둘째 인자는 일정한 수를 받습니다. 이후 두번째 인자만큼 많은 수들을 구하는 것이죠. 말로 푸니 어렵네요. 문제와 예시를 보여드리겠습니다.

### LeetCode 347. Top K Frequent Elements

##### 문제

```markdown
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.
```

##### 예시 1

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

##### 예시 2

```
Input: nums = [1], k = 1
Output: [1]
```

#### 내 답변

```js
var topKFrequent = function (nums, k) {
  const obj = {};
  let sortable = [];
  let result = [];

  for (i = 0; i < nums.length; i++) {
    obj[nums[i]] ? (obj[nums[i]] += 1) : (obj[nums[i]] = 1);
  }

  for (var number in obj) {
    sortable.push([number, obj[number]]);
  }

  sortable.sort(function (a, b) {
    return b[1] - a[1];
  });

  for (j = 0; j < k; j++) {
    result.push(+sortable[j][0]);
  }
  return result;
};
```

답을 찾았지만 JS 이용자 기준 하위 5%에 달하는 연산속도와 데이터 소모량을 보여줬습니다... 개선할 여지가 많아 보이지만 뚜렷한 해결책이 보이진 않았습니다. 요새 객체를 중점으로 생각하는터라 이번 문제 역시 객체를 기준으로 두고 각 숫자를 키 값, 반복 회수를 value로 두는 방식으로 해결했습니다

#### 우수 답변

```js
const topKFrequent = (nums, k) => {
  const map = {};
  const result = [];
  const bucket = Array(nums.length + 1)
    .fill()
    .map(() => []);

  for (let num of nums) {
    map[num] = ~~map[num] + 1;
  }

  for (let num in map) {
    bucket[map[num]].push(parseInt(num));
  }

  for (let i = nums.length; i >= 0 && k > 0; k--) {
    while (bucket[i].length === 0) i--;
    result.push(bucket[i].shift());
  }

  return result;
};
```

이번 우수 답변은 leetcode에서 가장 좋아요를 많이 받은 JS의 답변입니다. 그러나 지금도 100% 정확한 이해를 하고 있다고 확신하지 못하겠습니다. 그럼에도 빈 bucket에 숫자를 하나 하나 담아가는 해결책은 정말 아름답네요.
