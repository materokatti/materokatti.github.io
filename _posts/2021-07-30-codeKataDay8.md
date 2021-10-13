---
layout: single
title: "CODEKATA Day 8 [JS] - Leetcode 11번 문제풀이"
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

오늘 문제는 리츠코드의 11번 문제로 막대 그래프 형태의 숫자 배열 중 가장 넓은 조합을 추출하는 문제입니다. 문제를 정확히 이해하기 위해서는 이미지를 확인하는 것이 좋습니다. 하단에 링크를 첨부해 두겠습니다.

(https://leetcode.com/problems/container-with-most-water/ : 예시이미지를 보려면 링크를 클릭해주세요.)

### LeetCode 11. Container With Most Water

##### 문제

```markdown
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.
```

##### 예시 1

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

##### 예시 2

```
Input: height = [1,1]
Output: 1
```

##### 예시 3

```
Input: height = [4,3,2,1,4]
Output: 16
```

##### 예시 4

```
Input: height = [1,2,1]
Output: 2
```

#### 내 답변

```js
function getMaxArea(height) {
  const map = {};
  let arr = [];
  for (i in height) {
    map[i] = height[i];
  }

  for (i in map) {
    for (j in map) {
      v = Math.min(map[i], map[j]);
      arr.push((i - j) * v);
    }
  }
  return Math.max(...arr);
}
```

문제의 정답을 도출하는 코드는 작성을 했습니다. 그러나 제한 시간을 통과하지 못해서 오답이었죠. 각 그래프 중 2개를 추출해 반복문으로 모든 넓이를 구하는 조합입니다. 보시면 밑변의 조합에 따라 음수까지 나오는 굉장히 허술한 코드입니다. 거의 100가지가 넘는 경우를 구해 최대 넓이를 찾아내는 방식입니다.

#### 우수 답변

```js
var maxArea = function (height) {
  var maxArea = 0;
  var length = height.length;
  var head = 0,
    tail = length - 1;
  while (tail - head > 0) {
    var area = Math.min(height[head], height[tail]) * (tail - head);
    maxArea = Math.max(maxArea, area);
    if (height[head] > height[tail]) {
      tail--;
    } else {
      head++;
    }
  }
  return maxArea;
};
```

이번에도 JS 최대 좋아요를 받은 답변입니다. 정말 대단한 접근이라고 감탄한 답변입니다. 쉽게 말하면 양 밑변을 최대
