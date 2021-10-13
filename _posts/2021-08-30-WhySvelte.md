---
layout: single
title: "왜 Svelte를 써야할까?"
description: "Svelte.js에 대한 Chris Harris의 강좌 요약"
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

강좌 원본: https://www.youtube.com/watch?v=AdNJ3fydeao

이번 글은 Svelte.js를 만든 Chris Harris의 2019년 강의를 요약한 것입니다.

#### 상호 작용하는 프로그램

LANPAR technology를 아시나요? 이들은 1969년 forward referencing 이라는 동적인 스프레드 시트를 처음 만듦니다. 쉽게 말해 SUM 함수 같이 c 값이 a, b 값이 변함에 따라 동적으로 반응하는 프로그래밍인 것이죠. 당시 컴퓨터는 너무 느렸기 때문에 모든 스프레드 시트를 랜더링하기보다 부분 부분 필요한 요소만 랜더링 해준 겁니다. 혁신적인 시도였지만 성공하지 못했습니다. 오히려 1979년 등장한 VISICALC가 더 큰 성공을 거두게 됩니다. 애플에도 탑재된 VISICALC는 그러나 forward referencing을 사용하지 않았습니다. 하나 하나 일일이 수정해주는 작업으로 매우 느렸죠. 1983 forward referencing을 사용한 Lotus 1-2-3이 등장하면서 VISICALC는 잊혀집니다.

#### Reactivity를 다시 생각하다.

Reactive Programming이란 무엇일까요? 값이 선언되는 동시에 다이나믹한 변화를 보여주는 것이 Reactive이라고 합니다. 프론트 엔드 개발의 프레임워크들은 이런 동적인 상호작용을 효과적으로 구현하기 위해 만들어졌죠. 2013년 React가 등장한 이유 역시 마찬가지였습니다. 리엑트의 등장은 놀라운 혁신이었습니다. 또한 리엑트 팀은 다양한 개선을 통해 우리가 알지 못하던 오류들과 불편함을 개선했죠. 그럼에도 우리는 더 나아갈 수 있다고 믿습니다.

리엑트가 처음 등장한 시기 그들은 당시의 Framework를 강하게 비판하면서 등장합니다. 저 역시 그 멋진 전통을 이어갈까 합니다. 리엑트는 가상 DOM을 이용합니다. 이는 굉장히 비효율적이죠. 바꿔야 하는 것은 state값 하나이지만, 이를 위해 랜더링되는 모든 요소를 확인해야 합니다. 비효율적이죠.

즉, 엄밀히 말하면 React는 reactive 하지 못합니다. 변화가 선언됨과 동시에 다이나믹을 구현하지 못하고, 대신 모든 요소를 읽어야 하기 때문이죠. 이렇게 reactive 하지 못하고 비효율적인 프래임워크들을 개선하기 위해 전 Svelte라는 프로젝트를 시작했습니다.

#### 무엇이 변하는가?

svelte를 시작하며 가장 처음 한 고민은 '어떤 요소들이 변화하는지 어떻게 감지할 것인가'였습니다. 우리도 React 처럼 state를 정하고 setState로 변화를 주는 형태를 생각했죠. 그러나 너무 번거로웠습니다. 그래서 그냥 적어주는 방식을 선택합니다.

```javascript
let count = 0;

//later ..
count += 1;
```

마치 Vue.js에서 작동하는 방식과 비슷하죠. original JS에서 함수로 선언해줘야 하는 부분도 bind, on:event로 상당부분 단순화 되었습니다. 또한 Server Side Randering에서도 변화하는 부분만 처리하면 되기 때문에 부하가 덜 걸립니다. 즉, AWS에 납입하는 금액이 적어지는 것이죠. 아무튼 이런 방식으로 우리는 변화하는 부분을 감지했습니다.

#### 어떻게 변화시킬 것인가?

아직은 reactive하지 못합니다. 이제 이 변화되는 요소들을 다이나믹하게 그려줘야 했죠. React의 경우는 state값의 변화마다 계속 랜더링을 해주고 선언하기 때문에 고민이 적었죠. 그러나 Svelte의 경우 변화하는 요소만 재 랜더링 해주는 시스템으로 보다 까다롭습니다. 특히 const의 경우 한 번 선언되고 변화하지 않기 때문에 선언된 변수와 함수에 다이나믹을 제공하는 것을 어려웠죠.

우리는 외부에서 힌트를 얻었습니다. spreadsheet적인 반응을 구현한 Observablehq.com과 Paul Stovell에게서 힌트를 얻었죠. 그리고 Javascript의 Labelled Statement를 참조해 svelte만의 변화 syntex를 구성합니다.

```javascript
let a = 10;
$: b = a + 1;
```

이렇게 구성하면 b는 a에 묶이게 됩니다. 이 달러 요소를 react의 const 요소 대신 써주면 변화가 다이나믹하게 재현되죠. 리엑트처럼 수많은 랜더링이 전재되지 않기 때문에 더 빠르고 부드러운 UX 구현이 가능합니다.

#### UX 개선 효과

React의 경우 동기화, debouncing의 경우 다양한 문제가 발생하며, 그나마 둘을 결합한 비동기적 작동 방식이 부드러운 UI 구성을 돕습니다. 그럼에도 변화 요소가 증가할 수록 피할 수 없는 지연현상이 발생하죠. 그러나 svelte는 동기, 비동기와 상관 없이 훨씬 빠르고 이를 통해 차별화된 UX를 제공합니다. 가장 효과적으로 프로그래 구동을 개선하는 일은 코드를 줄이는 것입니다. svelte는 더 적은 코드로 reactive를 제공하죠. 데스크톱 웹이 주류이던 시대는 지났습니다. 모바일 웹의 전성기이지만 이미 많이 진행되었죠. 앞으로의 세상은 embedded web 즉 웨어러블, 스마트폰, IoT 기기에게 제공되는 web app이 중요해질 것입니다. 우리에겐 더 효과적인 수단이 필요합니다.

#### 스타일링을 위한 장점들

스타일링이 없는 웹 앱을 구축하는 경우는 없죠. 스타일링은 프론트엔드 웹 개발의 중요한 부분이지만, 라이브러리에서 이를 제공하는 경우는 거의 없습니다. svelte는 javascript 파일 내부에서 style을 함께 제어할 수 있도록 제공합니다. 이로써 style에 대한 관리를 코드와 함께 진행할 수 있어 간편하죠. 또한 다양한 패키지를 통해 transition, animation 등 효과를 쉽게 구현할 수 있도록 도와줍니다.

#### Svelte를 넘어서

스벨트는 더 가볍고 빠르게 구동되는 App을 지향합니다. 컴파일러로서 사용하지 않는 요소들은 제외하고 작동시키는 가벼움도 그 장점이죠. 점점 더 발전할 Svelte를 위해 우리는 몇가지 프로젝트를 추가로 진행하고 있습니다. Sapper, Svelte Native, Svelte GL등 Svelte를 더욱 효과적으로 활용할 시도가 계속되고 있죠.

요약하면 Spread Sheets의 간결한 Reactive로 돌아가자는 것입니다. 가독성이 좋고 Javascript적인 Svelte는 어떤 기술을 배운 누구에게든 편리할 겁니다. Svelte를 통해 웹 app을 개발하는 모두가 더 편하고 가까워지는 계기가 되길 바랍니다.
