---
layout: single
title: "CSS 포지션 쉽게 이해하기"
description: "CSS 포지션의 각 용법들을 쉽게 이해해 봅시다."
tags: [CSS]
comments: true
published: true
categories: CSS
sitemap:
  changefreq: daily
  priority: 1.0
---

CSS를 처음 배워가는 입장에서 컨텐츠 배열을 위한 박스, 포지션, 디스플레이 개념이 뚜렷하게 잡혀있지 않아 많이 햇갈리는데요. 오늘은 CSS에서 포지션에 대해서 명확하게 이해하려고 합니다. 처음 CSS를 배우는 분들과 훗날 다시 한번 점검할 제 자신을 위해 간략하고 본질에 충실하게 기록해 보겠습니다.

### 포지션의 기본 개념

CSS에서 포지션은 내가 화면상의 요소(element)를 어떤 형식으로 배치(positioning)할지를 결정합니다. 즉 position 뒤에 오는 다른 값들(static, relative, initial, absolute, fixed, 또는 sticky)에 따라 배열이 결정되는 것입니다. 말로 하면 어려우니 코드와 결과물을 통해 확인해 보겠습니다.

```html
<body>
  <h1>CSS 포지션 이해하기.</h1>
  <div class="outside">
    <div class="inside"></div>
  </div>
</body>
```

기본 세팅은 위의 코드로 하겠습니다. 코드를 풀이하면, 화면에는 하나의 <div>가 존재합니다. 그 안에는 또 하나의 <div>가 있는 구조입니다. 둘을 구분하기 위해서 외부의 <div>는 "outside"라는 class 값을 가집니다. 내부의 <div>도 마찬가지로 "inside"라는 class 값을 주겠습니다.

```html
<style>
  div.outside {
    border: 10px solid #f5b362;
    height: 500px;
    width: 1000px;
  }
  div.inside {
    border: 10px solid #de64a9;
    height: 200px;
    width: 200px;
    /* position: ; */
  }
</style>
```

상단의 코드는 CSS 기본세팅입니다. 아직 position 값은 입력하지 않겠습니다.

### static

가장 먼저 설명할 position의 용법(method)는 static입니다. static은 영어로 '정적이다'는 의미입니다. 이것은 position 속성의 사용법의 기본값(default)이기도 합니다. 즉 이를 position을 사용하지 않더라도 기본적으로 static을 이용해 요소들이 배열되는 것이죠. static은 정적이다는 의미에 걸맞게 요소가 원래 있어야 하는 기본 위치에 놓이게 합니다. left, right, top, bottom을 이용해 요소를 이동시키더라도 static 값을 쓰면 움직이지 않습니다.

코드와 예시를 보겠습니다. 코드는 inside의 스타일만 수정하겠습니다.

```css
div.inside {
  position: static;
  left: 700px;
  top: 200px;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/2021-06-01-static.png)

### relative

반면 이 static 값을 relative를 이용하면 이동시킬 수 있습니다. relative는 영어로 상대적이라는 의미에 맞게 절대적 위치(static)가 아닌 지정한 값에 따라 상대적으로 변하는 위치에 놓입니다. 상대적이라는 표현이 사용된 이유는 부모에 대해서 상대적이라는 의미입니다. 즉 위치 값에 따라 상대적으로 정해지는 위치인데 부모 요소, 혹은 상위 요소를 기준으로 상대적이라 relative라는 이름이 된 것이죠. 우리는 이것을 통해 원하는 위치로 요소를 이동시킬 수 있게 됩니다.

마찬가지로 코드와 예시 이미지를 보겠습니다.

```css
div.inside {
  position: relative;
  left: 700px;
  top: 200px;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/relative.png)

### absolute

다음은 absolute입니다. relative가 부모와 상대적인 위치로 이동을 시킨다면, absolute는 부모와 자식 요소간의 관계를 끊어 버립니다.(잔인하네요) absolute로 지정되면 포지션의 디폴드 값인 static인 모든 부모 요소들은 자식들에게 영향을 미치지 못합니다. 만약 상단의 부모 요소에서 relative 등 static이 아닌 position 값을 가진 부모가 나타나면 그곳을 기준으로 상대적인 위치를 가집니다. 말로하면 굉장히 어렵기 때문에 코드를 통해 보여드리겠습니다.

먼저 position이 relative인 상태에서 left : 0, top: 0 값을 주었습니다.

```css
div.inside {
  position: relative;
  left: 0;
  top: 0;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/relative-0-0.png)

보는 것처럼 left와 top값이 부모 상자인 outside 기준으로 배열됩니다. 이것이 relative로 부모 요소에 상대적인 위치값을 가집니다.

반면

```css
div.inside {
  position: absolute;
  left: 0;
  top: 0;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/absolute.png)

absolute는 앞에 지정되어 있는 position: static 요소와의 관계를 모두 꾾어버립니다. position의 디폴드 값이 static이기 때문에 position 값이 설정이 안되어 있는 경우도 모두 건너 뛰게 되죠. 그럼 한번 상위 요소를 더해보겠습니다.

```html
<div class="grand-outside">
  <div class="outside">
    <div class="inside"></div>
  </div>
</div>
```

이 HTML 구조에 style도 바꿔보겠습니다.

```css
div.grand-outside {
  position: relative;
}
div.inside {
  position: absolute;
  left: 0;
  top: 0;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/absolute-2.png)

보시다시피 absolute로 인해 상위 요소인 outside와의 관계는 끊어집니다. 다만 outside의 상위 요소인 grand-outside에 relative 값이 지정되었기 때문에 grand-outside에 상대적인 위치로 이동하는 것이죠. 즉 여기서 grand-outside에도 position 값이 없었더라면 HTML 최상단으로 이동했을 것입니다.

> 너무 복잡하면 absolute는 상위 요소가 static 포지션일 경우 그들과의 관계를 끊어준다 정도로만 인지하셔도 좋습니다.

### Fixed

Fixed 역시 문자 그대로 고정되어 있는 포지션을 나타냅니다. 이는 설명하는 것보다 눈으로 직접 확인하면 더 쉽게 이해 할 수 있습니다. 바로 예시를 살펴 보겠습니다.

먼저 html구성을 조금 변경하겠습니다.

```html
<div class="wallpaper">
  <div class="outside">
    <div class="inside"></div>
  </div>
</div>
```

Outside와 inside를 wallpaper로 감싸줬구요.

```css
div.wallpaper {
  width: 100%;
  height: 20000px;
}
```

div.wallpaper의 css 값은 위와 같이 설정했습니다. height를 20000px로 넣은 wallpaper를 만든 이유는 스크롤이 가능하도록 변경해야 하기 때문이죠.

그럼 이제 fixed를 적용하겠습니다.

```css
div.inside {
  position: fixed;
  left: 0;
  top: 0;
}
```

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/fixed.gif)

Fixed의 효과가 보이시나요? 이렇게 원하는 요소를 화면상 특정한 위치에 고정시키는 것이 fixed의 역할입니다. 화면상 어떠한 부모 요소에게도 영향을 받지 않기 때문에 absolute와 마찬가지로 관계를 단정하는 역할도 수행합니다.

![](https://raw.githubusercontent.com/tec-motive/tec-motive.github.io/master/_posts/imges/2021-05-30/fixed-2.gif)

Fixed는 모바일이나 웹페이지 상단에 매뉴바 혹은 특정한 버튼을 고정해 두는 역할을 수행하기 때문에 굉장히 많이 사용되는 position 용법입니다. 다른 많은 position의 용법들이 있지만 오늘은 이 정도로 마무리 하겠습니다.

#### 주의!

absolute와 fixed의 경우 부모와의 관계가 단절되기 때문에 스스로 크기(height, width)를 가질 수 없습니다. 즉 이들에게 개별적으로 height, width를 할당해 줘야 크기가 표현되는 것입니다. 상단의 absolute와 fixed의 예시 역시 제가 style.css를 통해 크기를 설정해 두었기 때문에 깔끔하게 보여질 수 있었습니다. 하단에 예시의 style.css를 첨부해두겠습니다.

```css
html {
  background-color: #d0eb5e;
}
div.outside {
  border: 10px solid #f5b362;
  height: 500px;
  width: 1000px;
}
div.inside {
  border: 10px solid #de64a9;
  height: 200px;
  width: 200px;
}
```
