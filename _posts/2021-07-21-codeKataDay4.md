---
layout: single
title: "CODEKATA Day 4 [JS] - Leetcode 3번 문제풀이"
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

### 3th - Longest Substring Without Repeating Characters

##### 문제

```markdown
Given a string s, find the length of the longest substring without repeating characters.
```

##### 예시 1

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

##### 예시 2

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

##### 예시 3

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

##### 예시 4

```
Input: s = ""
Output: 0
```

반복되는 서로 다른 알파벳 문자열의 최대값을 구하는 문제입니다. 단순해 보이지만, abcabc등 중복해서 반복되는 경우를 정리해줘야 하고, pwwkew처럼 최대값이 뒤에있는 경우도 정지해줘야 하기 때문에 시간이 걸리는 문제였습니다. 오전 내내 붙잡고 있었던것 같네요. 일반적인 배열을 통한 접근보다, object를 만들어주고 key 값과, value값을 나눠 정리해주는 방법을 선택했습니다. 접근은 좋았지만 반복문을 구성하는 과정에서 여러 실수가 있었고, 초기값(start)에 1을 더해주지 않아서 오류가 나기도 했습니다. 어찌저찌 해결은 되었습니다.

#### 내 답변

```js
const getLengthOfStr = function (s) {
  let start = 0,
    maxLength = 0;
  let map = new Map();

  for (let i = 0; i < s.length; i++) {
    let ch = s[i];

    if (map.get(ch) >= start) {
      start = map.get(ch) + 1;
    }
    map.set(ch, i);

    if (i - start + 1 > maxLength) {
      maxLength = i - start + 1;
    }
  }

  return maxLength;
};
```

오랜 시간을 고민했던 문제라 그런지 나름 개인적으로는 만족하고 있습니다. for문과 if문의 반복을 피하려고 했지만 그것을 제외한 해결 방법이 떠오르지 않았습니다.

#### 고수의 답변

```js
function lengthOfLongestSubstring(s) {
  const map = {};
  var left = 0;

  return s.split("").reduce((max, v, i) => {
    left = map[v] >= left ? map[v] + 1 : left;
    map[v] = i;
    return Math.max(max, i - left + 1);
  }, 0);
}
```

단 아홉줄만에 끝내버린 답변입니다. 제가 불편하게 생각한 반복문과 조건문의 반복 구조로 없는 신선한 답변입니다. Reduce함수에 콜백을 설정해 최대값을 제어하고 있습니다. 사실 아직도 100%이해 했다고는 말하기 어려운 답변입니다. 더 콘솔을 찍어보고 reduce에 대해 공부한 후에 한 번 더 이해해 보려고 합니다. 한 눈에 이해는 되지 않지만 새로운 방법으로 접근한 발상이 매력적이었습니다.
