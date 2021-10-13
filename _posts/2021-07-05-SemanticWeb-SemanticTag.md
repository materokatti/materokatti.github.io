---
layout: single
title: "사이트에 이미지를 넣는 두 가지 방법과 그 활용의 차이"
description: "Semantic Web과 Semantic Tag의 이해"
tags: [CSS]
comments: true
published: true
categories: CSS
sitemap:
  changefreq: daily
  priority: 1.0
---

> 사이트에 이미지를 넣을 때 어떤 태그를 사용하시나요?

일반적으로 이 질문에 답변을 떠올리면 <img>를 떠올리시기 쉽겠죠. 태그 이름 자체도 img이면서, HTML에 직접 입력하면 되는 굉장히 간단한 태그입니다.

그러나 이 방법만 있는 것은 아니죠.

```html
<div style="background-img: url(./img/imgFile.jpeg)></div>
```

이런 형식 역시 인지합니다. 즉 CSS를 통해 Background-img를 활용하는 방법도 있는 거죠. 이제 의문이 생길 수 있습니다.

> 왜 이미지를 올리는 방식은 이렇게 두 가지나 있는 것일까?

두 방식의 목적은 같습니다. 사이트에 이미지를 업로드 하는 것. 그러나 그 형태가 다릅니다. 이 형태/형식의 차이를 이해하려면 먼저 Semantic Web, Sementic Tag라는 두 녀석을 이해해야 하죠.

### Semantic Web? Semantic Tag?

낯설 수 있는 녀석들입니다. 그러나 말을 풀어보면 상당히 단순합니다. 우리는 웹과 태그의 의미를 알고 있으니 Semantic의 의미를 알아볼까요?

> Semantic == 의미론적인

즉 Semantic Web은 의미론적인 웹, 태그는 의미론적인 태그를 의미하는 것입니다. 과거에 HTML은 단순히 무의미한 태그로 구분되어 있었습니다. 이 태그에는 대표적으로 div와 span이 속합니다. 이런 무의미한 태그로도 header, main, footer등을 class값으로 할당하면 이해하는데는 문제가 없긴 하죠. 다만 이는 컴퓨터가 이해할 수 있는 방식이 아닙니다.

쉽게 말해서 Semantic Web은 컴퓨터가 이해 가능한 방식의 웹 구축, 그리고 이를 위해 컴퓨터가 이해 가능한 의미론적인 태그를 사용하는게 Semantic Tag입니다. 우리가 div와 span으로 구축한 웹 사이트는 사람이 무엇이 Header, main, footer인지 일일이 재 해석을 해줘야 이해가 가능합니다. 이러한 인간의 개입 없이 컴퓨터 자체가 해석이 가능한 태그가 Semantic Tag입니다. 이 태그들은 <header>,<nav>,<footer>등 태그 자체가 용도의 정보까지 함께 가지고 있습니다. 이로 인해서 컴퓨터가 홀로 사이트의 header만 모아 보고 싶더라도 인간의 해석 없이 홀로 실행 할 수 있는 것이죠. 컴퓨터의 관점으로 생각하면 놀라운 도약이죠. 이제 태그만 보고도 사이트에서 그 태그가 사용되는 방식을 알게 된 것입니다.

### Img & background-img

위의 의미론적 태그를 이해하면 <img>가 의미론적인 방식이고, background-img는 그렇지 못함을 이해 할 수 있습니다. 즉 기계의 입장에선 img는 그것이 img임을 설명해줍니다. 그러나 background-img는 비의미론적 태그에 스타일에 불과하기 때문에 인간의 개입이 필요합니다.

그렇다고 의미론적 태그인 img가 우월한 것은 아닙니다. HTML자체에서 정보량을 가지기 때문에 만약 HTML만 보고 판단을 해야하는 상황이라면 의미론적 태그가 앞도적으로 실용적입니다. 그러나 CSS를 관리하거나 hover등의 효과로 이미지를 전환 혹은 의도적인 왜곡이 필요하다면 CSS에서 제어하는 방식이 더 유연한 대처가 가능합니다. 결국 활용할 목적에 따라서 어떤 것이 좋은 방식인지 개발자 스스로 고민하고 선택해야 하는 것이죠.
