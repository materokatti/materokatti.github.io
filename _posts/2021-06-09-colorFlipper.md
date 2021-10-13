---
layout: single
title: "Javascript를 이용한 배경화면 변경 버튼"
description: "웹페이지의 배경화면 변경 버튼을 Javascript로 만들어봅시다."
tags: [Javascript]
comments: true
published: true
categories: Javascript
sitemap:
  changefreq: daily
  priority: 1.0
---

오늘은 자바 스크립트를 이용해 배경의 색상을 바꾸는 버튼을 만들어 보려고 합니다.

이 프로젝트는 바닐라 자바스크립트(라이브러리 등 부가적 기능을 제외한 순수한 javascript를 의미)를 이용한 단순한 프로젝트입니다.

전 이 프로젝트를 utube 영상을 통해 알게 되었는데요. (영상링크 :https://www.youtube.com/watch?v=3PHXvlpOkf4&t=28930s)

이것을 제외하고도 총 15개나되는 간단한 바닐라 자바스크립트를 모아뒀습니다.

혹 자바스크립트를 공부하시고 싶다면 좋은 소스가 될 것 같네요.

그럼 본격적으로 시작해보겠습니다.

### 1. 프로젝트 결과물

결과물 링크 : https://tec-motive.github.io/doyun-home/project01/hexColorFlipper/index_hexColorFlipper.html

링크가 결과물의 모습입니다.

프로젝트 제작자는 바닐라 자바스크립트 프로젝트로 이것을 구상했습니다.

때문에 자바스크립트이외의 HTML, CSS의 요소들은 모두 기본 세팅을 해줬습니다.

제작자의 결과물 및 세팅 자료도 영상을 통해 찾아보실 수 있습니다.

그럼 먼저 HTML 구조를 빠르게 확인하고 넘어가겠습니다.

### 2. HTML 구조

```html
<body>
  <nav>
    <div class="nav-center">
      <h4>color flipper</h4>
      <ul class="nav-links">
        <li><a href="index.html">simple</a></li>
        <li><a href="hex.html">hex</a></li>
      </ul>
    </div>
  </nav>
  <main>
    <div class="container">
      <h2>background color : <span class="color">#f1f5f8</span></h2>
      <button class="btn btn-hero" id="btn">click me</button>
    </div>
  </main>
  <!-- javascript -->
  <script src="app.js"></script>
</body>
```

먼저 index.html의 body입니다.

상단의 nav와 하단의 main으로 크게 나뉘에 있는게 보입니다.

그리고 nav의 내용물을 nav-center로 묶고 안에 <h4>와 simple, hex를 선택할 수 있는 list를 만들었습니다.

(simple과 hex는 제작자가 만든 구조인데, simple은 지정해둔 4가지 색상만 바뀌도록 되어있고, hex는 모든 색상이 조합되도록 만들었습니다. 말 그대로 simple은 간단한 버젼이죠)

하단의 main은 먼저 container용 div를 만들어주고 어떤 색이 결정되었는지 보여주는 h2태그를 붙였습니다.

마지막으로 모든 것의 하단에 버튼을 달아 유저의 반응에 상호작용하도록 했죠.

자바스크립트 프로젝트인 만큼 버튼을 통한 상호작용이 가장 중요하고, 이에 따라 변화하는 요소가 배경의 background-color값이 될 것이다 라는 점만 인지해두면 될 것 같네요.

그럼 HTML은 이만 줄이고 자바스크립트로 넘어가겠습니다.

### 3. Javascript 적용

먼저 우리가 만들어볼 배경 전환은 simple 버젼입니다.

즉, 정해진 4개의 색상으로만 전환이 가능한 구조를 만드는 것이죠.

HTML하단에 추가한 app.js를 통해 HTML을 자바스크립트로 제어할 수 있습니다.

<script src="app.js"></script>

그럼 제어를 위해 app.js를 하나 하나 살펴보겠습니다.

자바스크립트의 가장 단순한 구조는

- Selectors
- Event Listners
- Functions

로 3등분된 구조입니다.

이번 프로젝트 역시 이 구조를 가지고 있죠.

먼저, selector 부터 살펴보겠습니다.

#### 3-1. Selector

```javascript
const colors = ["green", "red", "rgba(133,122,200)", "#f15025"];
const btn = document.getElementById("btn");
const color = document.querySelector(".color");
```

총 3개의 변수를 생성했는데요.

처음 colors는 고정된 4가지 색을 가진 변수입니다.

btn은 document.getElementById("btn")을 이용해서 html의 id = "btn"의 값을 가져옵니다.

```
<button class="btn btn-hero" id="btn">click me</button>
```

즉, const btn에는 id = "btn"을 가지는 main의 button이 되는 것이죠.

다음인 color는 document.querySelector를 통해서 class값이 color가 할당된 요소를 가져옵니다.

여기서 querySelector는 특정한 값의 지정자(selector)를 가지는 document의 첫번째 요소를 가져옵니다.

즉 다수의 요소가 document내에 있더라도 첫번째 값을 가져오는 것이죠.

#### 3-2. Event Listener

```javascript
btn.addEventListener("click", function () {
  const randomNumber = getRandomNumber();
  document.body.style.backgroundColor = colors[randomNumber];
  color.textContent = colors[randomNumber];
});
```

다음은 Event Listener입니다.

이 프로젝트에는 버튼 이외에 효과가 없기 때문에 버튼의 'click'에 반응하는 eventListener만 추가해줬습니다.

btn즉 버튼이 눌리면 listner 내부에서 함수가 실행됩니다.

함수는 즉시 randomNumber라는 지역변수를 선언하고 getRandomNumber()라는 함수를 할당하죠.

getRandomNumber()는 무작위 숫자를 구하는 함수인데, 마지막 파트에서 설명드리겠습니다.

이어서 document.body.style.backgroundColor는 적힌대로 document의 style에 속한 배경 색상으로 연결합니다.

이것을 colors의 색상을 무작위로 즉, randomNumber로 할당함으로서 4개의 색상 중 임의의 색상이 선택됩니다.

그리고 color (즉, html의 main에서 색상의 이름을 설명해주는 h2 값의 span)에 택스트값 역시 colors의 무작위 색으로 변경해주죠.

이로써 버튼의 eventListener가 마무리됩니다.

#### 3-3 function

```javascript
function getRandomNumber() {
  return Math.floor(Math.random() * colors.length);
}
```

마지막으로 함수인데요 프로젝트가 단순해서 함수 역시 1개만 선언합니다.

앞서 살펴본 getRandomNumber() 함수입니다.

단순하게 return값에 math.random 함수를 이용해 0-1까지 임의의 수를 출력하고, 이를 color의 리스트 개수에 곱해 0-3까지의 숫자가 출력되도록 합니다.

여기에 math.floor를 통해 소수점을 제거해서 0,1,2,3 중 하나의 수 즉, 리스트 값 4개 중 하나를 무작위로 선택할 숫자가 세팅되는 것이죠.

### 4. Hex 무작위 출력 버젼

Hex 무작위 출력버젼의 경우 Html은 링크만 차이날 뿐 전반적인 형식은 동일하기 때문에 javascript만 살펴보겠습니다.

```javascript
const hex = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "A", "B", "C", "D", "E", "F"];
const btn = document.getElementById("btn");
const color = document.querySelector(".color");

btn.addEventListener("click", function () {
  let hexColor = "#";
  for (let i = 0; i < 6; i++) {
    hexColor += hex[getRandomNumber()];
  }
  // console.log(hexColor);

  color.textContent = hexColor;
  document.body.style.backgroundColor = hexColor;
});

function getRandomNumber() {
  return Math.floor(Math.random() * hex.length);
}
```

차이가 보이시나요?

4개의 색상 중 하나를 선택하는 것과 무작위 Hex를 추출하는 것의 차이는 크게 2가지로

- Hex 변수
- 임의의 hex를 추출하는 eventListener

이렇게 2가지 입니다.

둘을 나눠서 살펴보죠.

```
const hex = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "A", "B", "C", "D", "E", "F"];
```

먼저 hex 색상은 0-15까지의 구성이 이뤄지는데, 9이상의 숫자는 A - F로 표현합니다.

이것이 첫째 차이를 보이는 변수 선언이구요.

```javascript
btn.addEventListener("click", function () {
  let hexColor = "#";
  for (let i = 0; i < 6; i++) {
    hexColor += hex[getRandomNumber()];
  }
  color.textContent = hexColor;
  document.body.style.backgroundColor = hexColor;
});
```

둘째는 임의의 hex값인 hexColor에 대한 EventListener입니다.

전반적인 내용은 동일하지만, 계속 수정이되면서 입력값이 변해야 하는 변수를 선언해야 합니다.

즉 위에 보이는 hexColor는 '#'만 초기선언으로 존재하고 나머지 값은 hex 변수의 0-15 번째 요소중 하나씩 임의로 배정되는 것이죠.

이 때문에 #뒤로 요소가 하나 하나 추가되어야 합니다.

그러므로 할당 후 수정이 불가능한 const가 아니라 let을 선언해줍니다.

뒤이어 for문을 통해 6번에 걸쳐서 hex 변수값을 hexColor에 추가해주면 됩니다.

이 두 부분을 제외한 것은 모두 동일하기 때문에 이것만 주의하면 충분합니다.

이렇게 배경화면 바꾸기 버튼은 마무리 짓도록 하겠습니다.

다음 프로젝트로 금방 돌아오겠습니다.

감사합니다.
