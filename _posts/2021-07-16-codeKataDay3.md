---
layout: single
title: "CODEKATA Day 3 [JS] - Leetcode 9번, 13번 문제풀이"
description: "Leetscode 9번 문제풀이"
tags: [CODEKATA]
comments: true
published: true
categories: CODEKATA
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

### 9th - Palindrome Number

Given an integer `x`, return `true` if `x` is palindrome integer. An integer is a **palindrome** when it reads the same backward as forward. For example, `121` is palindrome while `123` is not.

##### 예시 1

```
Input: x = 121
Output: true
```

##### 예시 2

```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

##### 예시 3

```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

##### 예시 4

```
Input: x = -101
Output: false
```

9번 문제는 역순으로 읽어도 동일한 수인 회문 정수(palindrome integer)를 구분하는 함수를 구하는 것입니다. Day2의 마지막 문제에서 숫자를 string값으로 전환해 역으로 변환하는 과정을 사용했기 때문에 이번에도 무리없이 문제를 풀 수 있었습니다.

#### 내 답변

```js
var isPalindrome = function (x) {
  if (x < 0) {
    return false;
  } else {
    const reverse = x.toString().split("").reverse().join("");
    console.log(reverse);
    if (+reverse === x) {
      return true;
    } else {
      return false;
    }
  }
};
```

먼저 음수인 경우 false를 선언해줬구요. Else 뒤의 reverse 변수는 숫자를 분해하고 문자 상태에서 역으로 조합했습니다. 그리고 이를 숫자로 전환하는데 꼼수를 사용했는데요. JS에서는 문자 앞에다 연산자 기호를 붙이면 숫자로 전환됩니다. 이를 이용해 +reverse === x 로 숫자의 비교를 만들어봤습니다. 어려움은 없었지만 그래도 고수의 코드를 보고 싶었습니다.

#### 고수의 답변

```js
function isPalindrome(x) {
  if (x < 0) return false;
  if (x < 10) return true;
  if (x % 10 === 0) return false;

  let rev = 0;
  while (rev < x) {
    rev *= 10;
    rev += x % 10;
    x = Math.trunc(x / 10);
    // console.log(`rev : ${rev}, x: ${x}`) 이해가 되지 않으면 콘솔을 찍어보세요
  }
  return rev === x || Math.trunc(rev / 10) === x;
}
```

수학적 모델링이 간결한 코드에 얼마나 도움이 되는가를 깨닫게 된 코드입니다. 앞에 if문 3가지를 통해 1의 자리와 20, 100, 5550등 10의 자리로 떨어지는 경우를 모두 처리해버립니다. 단순하게 회문이 아닌 경우가 반복문까지 접근하지 못하도록 깔끔하게 처리했죠. 뒤에 while문의 경우 조금 이해하는데 시간이 걸렸는데요. 쉽게 말하면 숫자를 두 부분으로 조각내어 서로를 비교하는 것입니다. 예를 들어 1221인 경우 12, 12로 나눠서 비교하는 것이죠. rev에 10을 곱해 자리수를 밀어내는 방법을 택하다니, 수포자인 저로서는 경이로운 경험이었습니다. ㅎㅎㅎ..

### 13th - Roman to Integer

##### 문제

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```markdown
Symbol Value
I 1
V 5
X 10
L 50
C 100
D 500
M 1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

##### 예시 1

```
Input: s = "III"
Output: 3
```

##### 예시 2

```
Input: s = "IV"
Output: 4
```

##### 예시 3

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

##### 예시 4

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

다음 문제는 로마자 숫자를 더하는 문제입니다. 우리같은 동양인에겐 로마자 숫자 읽는 법을 모르는 경우가 많아 이해하는데 조금 시간이 걸렸습니다. 처음에 답변을 못하다가, 객체를 이용하면 좋겠다는 힌트를 얻어 해결했습니다. 시간이 생각보다 많이 걸린 문제였습니다.

#### 내 답변

```js
var romanToInt = function (s) {
  if (!s || s.length === 0) {
    return 0;
  }

  const map = new Map([
    ["I", 1],
    ["V", 5],
    ["X", 10],
    ["L", 50],
    ["C", 100],
    ["D", 500],
    ["M", 1000],
  ]);

  let i = s.length - 1;
  let result = map.get(s[i]);

  while (i > 0) {
    const now = map.get(s[i]);
    const next = map.get(s[i - 1]);
    if (next >= now) {
      result += next;
    } else {
      result -= next;
    }
    i--;
  }
  return result;
};
```

앞선 문제에서 고수의 답변에서 힌트를 얻어 먼저 자리수가 없는 인자는 제외하는 가정문을 넣었습니다. 이후에는 객체 map을 생성해 로마자를 숫자와 대응해 저장하고 자리수에 따라서 뒤에서 읽어오는 방향으로 해결했습니다.

#### 고수의 답변

```js
symbols = {
  I: 1,
  V: 5,
  X: 10,
  L: 50,
  C: 100,
  D: 500,
  M: 1000,
};

var romanToInt = function (s) {
  value = 0;
  for (let i = 0; i < s.length; i += 1) {
    symbols[s[i]] < symbols[s[i + 1]]
      ? (value -= symbols[s[i]])
      : (value += symbols[s[i]]);
  }
  return value;
};
```

이번 고수의 답변은 직관적으로 해석하기 매우 좋은 구조입니다. 제 코드와 비교하면 큰 차이가 보이네요. 특히 단순하게 객체 선언 조차도 독자가 읽기 편하게 깔끔하게 적어준 부분은 큰 영감을 받았습니다. 또한 뒤에 함수도 불필요한 변수 선언 없이 깔끔한 구성이 눈에 띕니다.
