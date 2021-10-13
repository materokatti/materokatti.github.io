---
layout: single
title: "CODEKATA Day 5 [JS] - Leetcode 14번 문제풀이"
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

오늘은 leetscode에 대한 문제 말고도 제가 공부하고 있는 위코드에서의 codeKata문제도 소개해드리겠습니다.

### 위코드 CodeKata Day 3

##### 문제

```markdown
숫자인 num을 인자로 넘겨주면, 뒤집은 모양이 num과 똑같은지 여부를 반환해주세요.

num: 숫자 return: true or false (뒤집은 모양이 num와 똑같은지 여부)

예를 들어, num = 123 return false => 뒤집은 모양이 321 이기 때문
```

##### 예시 1

```
num = 1221 return true => 뒤집은 모양이 1221 이기 때문
```

##### 예시 2

```
num = -121 return false => 뒤집은 모양이 121- 이기 때문
```

##### 예시 3

```
num = 10 return false => 뒤집은 모양이 01 이기 때문
```

#### 내 답변

```js
const sameReverse = (num) => {
  const reverseNum = num.toString().split("").reverse().join("");
  const strNum = num.toString();
  return strNum === reverseNum;
};
```

3줄만에 해결되는 간단한 문제였습니다. 문자열과 배열을 제어하는 메서드에 대한 이해만 있다면 어려운 문제는 아니었습니다. 여기에 JS가 가지고 있는 유연함 혹은 결함을 이용하면 한 줄을 더 줄일 수 있습니다.

```js
const sameReverse = (num) => {
  const reverseNum = num.toString().split("").reverse().join("");
  return strNum == reverseNum;
};
```

연산자 기호를 하나 제외하면 두 줄만에 끝나버립니다. 숫자와 스트링의 값을 유연하게 이해하는 자바스크립트의 특징을 통한 해결입니다. 그러나 엄밀한 정답이 아니기 때문에 '==='연산자를 사용하는 해결이 더 나아보입니다.

### LeetCode 14. Longest Common Prefix

##### 문제

```markdown
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".
```

##### 예시 1

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

##### 예시 2

```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

#### 내 답변

```js

```

40분 가량 생각했지만 결국 답변을 찾지 못했습니다. 추천 답변을 보고 느낀 오류는 모든 문자를 전부 비교하려고 고집해서 효율적인 코드 작성에 실패했다고 느꼈습니다.

#### 우수 답변

```js
function longestCommonPrefix(strs) {
  if (!strs.length) return "";

  for (let i = 0; i < strs[0].length; i++) {
    for (let str of strs) {
      if (str[i] !== strs[0][i]) {
        return str.slice(0, i);
      }
    }
  }

  return strs[0];
}
```

더 추천을 받은 답변들도 있었지만 가장 직관적이고 단순했기에 이 답변을 소개드립니다. 제가 매번 빠뜨리는 부분이 있습니다. 우수 답변들의 공통점은 코드 진입부에 만약 빈 인자가 입력된 경우 이를 전체 연산에서 제외하는 코드를 붙여주고 있습니다. 이를 통해 다양한 연산에 효과적으로 대응하고 있죠. 앞으로 빠뜨리지 말아야 할 중요한 부분입니다. 중복된 for문이 본격적인 문제 해결의 시작입니다. 여기서도 눈여겨 보아야 할 부분은 첫 for문의 반복 횟수를 첫 번째 인자의 길이로 제한한 것입니다. 모든 요소의 연산이 필요하지 않기 때문에 가장 경제적인 진입을 선택한 것이죠. 그 뒤에는 첫 요소의 문자와 두번째 세번째 인자의 같은 위치를 비교해줍니다. 직관적으로 이해하기 쉬운 해결 방안도 감동적이짐만, return을 3군데 선언하면서 빠져나갈 기회가 있으면 전체 연산을 피하는 경제적인 접근법은 분명 배워야 한다고 느꼈네요.
