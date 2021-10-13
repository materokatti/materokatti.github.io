---
layout: single
title: "component 생애 주기"
description: "component, lifecycle이란??"
tags: [React]
comments: true
published: true
categories: React
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0


---

 컴포넌트도 라이프 사이클, 즉 생애 주기를 가지고 있다는 것을 아시나요. 오늘은 초심자들에게 모호한 이 개념을 명확하게 하는 시간을 가지겠습니다.



#### 컴포넌트 생애주기에 따른 메서드

react에서 컴포넌트는 크게 3단계를 거쳐 활용됩니다.

- 생성될 때 : constructor, render, componentDidMount(컴포넌트가 올라오는 단계)
- 업데이트 할 때 : render( new props, setState, forceUpdate), componentDidUpdate
- 제거할 때 : componetWillUnmount (로그인 창에서 매인 창으로 넘어가는 것 같은 경우)



제가 측면에 기입해두었듯이 각각의 시점마다 활용되는 메서드가 있습니다. 크게 componentDidMount, componentDidUpdate, componetWillUnmount 가 있습니다. 이외에도 다양한 메서드가 있지만 크게 중요하진 않습니다. 함수형 컴포넌트를 사용하는 경우 하나의 함수로 처리되기 때문에 이를 알 필요는 없지만 class로 react 컴포넌트를 선언하는 경우 이 형태로 메서드들이 이용된다는 점 알아두시면 좋겠네요.



#### 라이프 사이클 기본 순서

 메서드들을 알아봤으니 기본적인 라이프 사이클 순서를 볼까요?



1. constructor
2. render
3. componentDidMount
4. (fetch 완료)
5. (setState)
6. render
7. componentDidUpdate (5번에서 setState 되었기 때문에 컴포넌트 업데이트 발생)
8. componentWillUnmount



 자 이형식으로 순차적으로 진행됩니다. componentDidMount는 render 뒤에 실행됩니다. componentDidUpdate는 setState로 업데이트 된 이후 발생하죠. componentWillUnmount는 컴포넌트가 사라지는 단계입니다. 가끔 이 순서에 대한 착각으로 undefined 된  요소에 map을 선언해 에러가 나기도 합니다. 이 경우 조건부 렌더링을 통해 해결이 가능합니다. 

 주목할 점은 만약 자식 컴포넌트가 있을 경우 자식의 render까지는 모두 돌고 첫 자식의 componentDidMount, 그리고 둘 째 자식의 componentDidMount 순으로 처리가 됩니다. 이는 리엑트가 가진 기본 규칙입니다. 이런 라이프 사이클은 디버깅에 중요하고 원하는 시점에 우리가 필요한 동작을 실행시키기 위해서 중요합니다.