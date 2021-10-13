---
<br>layout: single
title: "Javascript을 이용해 html에 태그 추가하기"
description: "Javascript을 이용해 html에 태그 추가하기"
tags: [Javascript]
comments: true
published: true
categories: Javascript
sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요 오늘은 Javascript을 이용해 html에 태그 추가하는 법을 알아보겠습니다. 오늘 음식 매뉴를 넣고 필터링하는 자바스크립트를 배웠는데요. 그 과정에서 app.js에 변수 입력을 통해 새로운 자료를 추가하는 것을 배웠습니다. 배우는 입장에서 신기한 경험이었습니다. 오늘은 이 방법을 공유해드릴게요 :)

### 1. 프로젝트 결과물

결과물 링크 : https://tec-motive.github.io/doyun-home/project01/menu/index.html

오늘도 진행한 프로젝트의 결과물 먼저 보겠습니다. 한국 음식을 소개하는 사이트를 구상해봤습니다. 상단의 필터 바를 통해 매뉴를 필터링 할 수 있습니다. 그러나 오늘 배운 가장 흥미로운 것은 필터링이 아니었습니다. app.js의 변수를 추가하는 방식으로 html에 구조를 추가하는 내용이었죠. 찬찬히 설명드리도록 하겠습니다.

### 2. HTML 구조

```html
<body>
  <section class="menu">
    <!-- title -->
    <div class="title">
      <h2>Korean Food</h2>
      <div class="underline"></div>
    </div>
    <!-- filter buttons -->
    <div class="btn-container">
      <!-- <button class="filter-btn" type="button" data-id="all">all</button>
      <button class="filter-btn" type="button" data-id="breakfast">breakfast</button>
      <button class="filter-btn" type="button" data-id="lunch">lunch</button>
      <button class="filter-btn" type="button" data-id="shakes">shakes</button> -->
    </div>
    <!-- menu items -->
    <div class="section-center">
      <!-- single itme -->
      <!-- <article class="menu-item">
        <img src="./menu-item.jpeg" class="photo" alt="menu item">
        <div class="item-info">
          <header>
            <h4>buttermilk pancakes</h4>
            <h4 class="price">$15</h4>
          </header>
          <p class="item-text">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Optio consequatur sapiente voluptate fugit
            asperiores facilis, reprehenderit aspernatur animi. Incidunt, expedita?
          </p>
        </div>
      </article> -->
      <!-- end of single item -->

    </div>
  </section>
  <!-- javascript -->
  <script src="app.js"></script>
</body>

</html>
```

길지만 생각보다 단순합니다. 주목해서 보셔야 할 부분은 <div class="btn-container">과 <div class="section-center">입니다. 이 두 블록의 하단이 크게 주석처리된 것이 보일 것입니다. 이는 프로젝트 이해를 위해 제가 추가한 것인데요. 원래는 주석의 내용처럼 버튼, 매뉴 내용물을 직접 입력해야 하죠. 그러나 오늘은 javascript를 통해 저 자리에 내용을 추가하는 법을 배우겠습니다.

### 3. Javascript 적용

이제 app.js를 살펴볼 겁니다. 찬찬히 하나씩 이해해보도록 하죠.

#### 3-1. Selector

```javascript
const menu = [
  {
    id: 1,
    title: "Kimchi",
    category: "side-dish",
    price: 4,
    img: "./images/kim-chi.jpeg",
    desc: `While there are many different kinds of kimchi, the most common version is made with napa cabbage that is preserved and lightly fermented in bright red chili flakes. Love kimchi and you’re on your way to being a Korean food connoisseur!`,
  },
  {
    id: 2,
    title: "Smagyeopsal",
    category: "pork",
    price: 8,
    img: "./images/samgyupsal.jpeg",
    desc: `Fatty slices of pork belly grilled before your nose is a South Korean foodie favorite. A few slabs of this ultra-tasty pork along with garnishes of lettuce leaves, garlic and chili paste, and you’ve got a flavor to cherish.`,
  },
  {
    id: 3,
    title: "Pork Bulgogi",
    category: "pork",
    price: 7,
    img: "./images/Pork-Bulgogi.jpeg",
    desc: `While it’s normally made from beef, bulgogi can also be made with thin strips of pork or chicken.
    Before the meat is grilled, it’s marinated in sweet soy sauce with lots of garlic and sesame oil.`,
  },
];
```

먼저 최상단에 붙는 변수입니다. 오늘 다룰 내용 중 가장 중요한 부분 중 하나입니다. 일단 변수를 생성해 배열을 저장한 것이 보입니다. id값과 타이틀, 카테고리 등 매뉴의 새부 정보가 보입니다. 이 세부정보들을 이용해 html로 자료를 추가할 겁니다.

```javascript
const sectionCenter = document.querySelector(".section-center");
const container = document.querySelector(".btn-container");
```

앞서 언급한 대로 하단에 블럭들을 추가해야 하는 녀석들도 변수로 생성해줍니다.

#### 3-2. EventListener

```javascript
//load items
window.addEventListener("DOMContentLoaded", function () {
  displayMenuItems(menu);
  displayMenuButtons();
});
```

이번 프로젝트에선 이벤트 리스너가 하나뿐입니다. 보시면 아시겠지만 DOMContentLoaded 즉 자료가 열리면 즉시 함수를 실행합니다. 함수는 2가지인데요. 매뉴를 생성해주는 함수와 그에 맞는 버튼을 만들어주는 함수로 나뉩니다. 이 두가지 함수가 조금 어렵기 때문에 바로 살펴보겠습니다.

#### 3-3. Function

먼저 디스플레이될 아이템을 결정해주는 함수입니다. 이놈의 역할은 우리가 만들고자 하는 html블록을 <div class="section-center"> 하단에 붙여주는 것이죠.

```javascript
function displayMenuItems(menuItems) {
  let displayMenu = menuItems.map(function (item) {
    return `<article class="menu-item">
  <img src=${item.img} class="photo" alt=${item.title}>
  <div class="item-info">
    <header>
      <h4>${item.title}</h4>
      <h4 class="price">$${item.price}</h4>
    </header>
    <p class="item-text">
      ${item.desc}
    </p>
  </div>
</article>`;
  });
  displayMenu = displayMenu.join("");
  sectionCenter.innerHTML = displayMenu;
}
```

한 눈에 알아보기엔 쉽지 않죠?그러나 어렵지 않습니다. 위에 먼저 파라미터 menuItems에게 .map 매소드를 사용한 것이 보입니다. map은 사용되는 배열의 각 요소마다 뒤의 함수를 적용 시킵니다. map의 콜백 함수를 보니

```javascript
function (item) {
    return `<article class="menu-item">
  <img src=${item.img} class="photo" alt=${item.title}>
  <div class="item-info">
    <header>
      <h4>${item.title}</h4>
      <h4 class="price">$${item.price}</h4>
    </header>
    <p class="item-text">
      ${item.desc}
    </p>
  </div>
</article>`
```

이렇게 되어 있군요. 아시겠나요? 즉 map을 통해서 모든 배열 값의 요소를 읽어오고 이를 우리가 만들고자 하는 블럭을 만들어주는데 사용하는 것입니다. 어려운 친구가 아니었네요.

```javascript
	displayMenu = displayMenu.join('');
  sectionCenter.innerHTML = displayMenu;
}
```

이제 displayMenu에는 긴 행렬들이 모여져있게 됩니다. 이들은 블럭, 블럭, 블럭 , ... 같은 구조로 되어 있기 때문에 바로 html에 적용하기 어렵죠. 이 때문에 join함수를 이용해 사이의 ','를 제거해 줍니다. 이러면 바로 html에 붙어도 문제가 없습니다. 마지막엔 innerHTML을 사용해 sectionCenter 하단에 붙여줍니다. 산을 하나 넘었네요. 이제 버튼을 만들어주는 함수입니다.

```javascript
function displayMenuButtons() {
  const categories = menu.reduce(
    function (values, item) {
      if (!values.includes(item.category)) {
        values.push(item.category);
      }
      return values;
    },
    ["all"]
  );
  const categoryBtns = categories
    .map(function (category) {
      return `<button class="filter-btn" type="button" data-id=${category}>${category}</button>`;
    })
    .join("");
  container.innerHTML = categoryBtns;

  const filterBtns = container.querySelectorAll(".filter-btn");

  filterBtns.forEach(function (btn) {
    btn.addEventListener("click", function (e) {
      const category = e.currentTarget.dataset.id;
      const menuCategory = menu.filter(function (menuItem) {
        //console.log(menuItem.category)
        if (menuItem.category === category) {
          return menuItem;
        }
      });
      if (category === "all") {
        displayMenuItems(menu);
      } else {
        displayMenuItems(menuCategory);
      }
    });
  });
}
```

솔직히 이 친구는 좀 어렵긴 합니다. 그러나 초반에는 다가가기 힘들어도 좋은 친구가 되는 경우가 많으니까요. 찬찬히 친해져보도록 하죠.

```javascript
const categories = menu.reduce(
  function (values, item) {
    if (!values.includes(item.category)) {
      values.push(item.category);
    }
    return values;
  },
  ["all"]
);
```

맨 상단에 reduce 매소드를 사용했는데요. map과 비슷하게 모든 요소에 대해 반응하지만 앞서 처리한 value값을 가져와 추가적으로 처리해준다는 점이 다릅니다. 맨 마지막에 있는 ["all"] 배열 뒤로 menu에 있는 카테고리를 추가해 주는 것입니다. 중간에 if문을 활용해서 item의 카테고리가 이미 value 값에 있으면 추가하지 않고, 없으면 추가해주는 구조입니다.

```javascript
const categoryBtns = categories
  .map(function (category) {
    return `<button class="filter-btn" type="button" data-id=${category}>${category}</button>`;
  })
  .join("");
container.innerHTML = categoryBtns;
```

그 하단에는 위에서 지정된 카테고리를 바탕으로 버튼을 만들어주는 것입니다. 매뉴를 붙여주던 것과 다를 것이 없죠. 한 가지 차이가 있다면 map내부에서 함수가 지정되어 그 뒤에 바로 join을 이용해 공백을 비워준 것입니다.

```javascript
const filterBtns = container.querySelectorAll('.filter-btn')

  filterBtns.forEach(function (btn) {
    btn.addEventListener('click', function (e) {
      const category = e.currentTarget.dataset.id;
      const menuCategory = menu.filter(function (menuItem) {
        //console.log(menuItem.category)
        if (menuItem.category === category) {
          return menuItem;
        };
      });
      if (category === "all") {
        displayMenuItems(menu)
      } else {
        displayMenuItems(menuCategory);
      };
    });
  });
};
```

이제 버튼의 반응을 제어해 줄 차례입니다. 버튼의 종류가 다수이기 때문에 querySelectorAll로 지정해줍니다. 그리고 그 때문에 .forEach(function (btn){})으로 함수를 적용해줘야 합니다. 버튼이 눌리면 그 데이터 셋 값의 id로 감지해 주는데요. 이 때문에 위에서 버튼 블록을 만들면서 데이터 id를 추가해줬습니다. 이를 바탕으로 누른 데이터값에 동일한 카테고리만 display 시켜주는 것이죠. 혹 all을 선택할 경우 모든 값을 그대로 출력해줍니다. 이 모든 과정은 if문을 통해 단순하게 구성했습니다.

변수와 파라미터값 때문에 조금 읽기 복잡하게 느껴질 수 있지만 천천히 확인해 보면 전혀 어렵지 않음을 느낄 수 있습니다. 오늘도 한 가지를 더 배웠네요 :)
