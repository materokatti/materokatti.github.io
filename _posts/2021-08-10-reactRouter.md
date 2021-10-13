---
layout: single
title: "React Router 심화"
description: "React Router에 대해 조금 더 깊게 이해해 봅니다."
tags: [React]
comments: true
published: true
categories: React
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---



 라우팅은 경로를 찾아가는 기능을 의미합니다. React는 자체적인 라우팅 기능이 없기 때문에 React-router-dom을 이용하는데요. 기본적인 라우팅 이외에도 여러가지 부가기능을 제공합니다. SPA는 페이지 간 이동시간을 느낄 수 있는 딜레이를 제거하는데 이에 결정적인 역할을 하는 것이 React-router-dom입니다. 오늘은 이 기능이 제공하는 기능에 대해 알아보겠습니다.

#### 정적 라우팅, 동적 라우팅

 일반적으로 활용하는 라우팅은 exact path를 이용해 "/main, /signin"등 주로를 명시해주는 정적인 라우팅이죠. 그러나 우리가 자주 사용하는 사이트의 URL을 보면 정적이지 않습니다. 숫자나 ?, & 등 특수기호가 잔뜩 붙은 형태로 구성이 됩니다. 이를 동적 라우팅이라고 부릅니다. 동적 라우팅은 또한 path parameter, 그리고 query parameter를 사용하는 방법으로 나뉘죠.



#### Path Parameter

```react
//정적
"/users/1" => <Users id={1} />

//동적(path parameter)
"/users/:id" => <Users /> // this.props.match.params.id
```

Path 파라미터는 정적 url에서 변화하는 부분을 :id 등으로 표기해줍니다. :id는 그 자리에 id가 들어올 것을 의마합니다. 다만 이 값은 변수이기 때문에 임의의 값을 변수로 넣어줄 수도 있습니다. 즉 product id 가 들어가도 상관 없는 것이죠. 



```react
this.props.history.push("/product/1")
```

위 코드처럼 이 위치에 들어가는 요소는 event를 이용해 this.props.history.push로 원하는 값을 전달해 줄 수 있습니다. Router-dom은 history, location, match라는 3가지 객체를 제공합니다. 이를 활용해 routing을 더 다채롭게 할 수 있는 것이죠. 예를 들어 history의 push등 페이지 이동을 위한 다양한 메서드도 이 객체에 담겨있죠. location의 경우는 현재 url에 대한 정보를 담고 있고, match는 path parameter에 관한 정보를 담습니다. 

 

 위 세가지 객체는 this.props에 담깁니다. 그러나 주의 할 점! Route.js에 직접적으로 연결되지 않은 컴포넌트의 경우 이 객체들을 제공받지 못합니다. 때문에 이렇게 분리된 객체에겐

```react
export default withRouter(Payment);
```

이렇게 export 과정에서 withRouter를 추가해줘야 합니다. 그래야 객체를 제공받을 수 있죠.



#### Query Parameter

```react
//정적
"/search?keyword=위코드"    : <Search keyword="tec-motive" />

//동적(query parameter)
"/search?keyword=something" : <Search /> // this.props.location.search
```

 쿼리 파라미터는 위 처럼 ? 형태로 묻고 & 형태로 더해지는 엔드포인트를 가집니다. 흔히 pagination이라고도 하는데요. 백엔드가 가진 데이터가 많기 때문에 일정한 길이로 끊어서 전달받는 과정입니다. 아래에 기본 개념들을 정리하겠습니다.



- '?' 기호는 쿼리스트링의 시작을 알립니다. url 에서 `?` 기호는 유일무이 합니다.
- **limit** : 한 페이지에 보여줄 데이터 수
- **offset** : 데이터가 시작하는 위치(index)
- `parameter=value` 로 필요한 파라미터의 값을 적습니다.
- 파라미터가 여러개일 경우 `&`를 붙여서 여러개의 파라미터를 넘길 수 있습니다.