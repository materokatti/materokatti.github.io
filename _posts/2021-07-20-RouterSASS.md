---
layout: single
title: "Router? Sass?"
description: "Router? Sass?"
tags: [React]
comments: true
published: true
categories: React
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요 오늘은 리엑트의 라우터와 SASS에 대해 간략하게 정리해보려고 합니다. 먼저 라우터에 대해 설명하겠습니다. 라우터가 하는 일인 '라우팅'은 하나의 화면에 여러가지 페이지를 보여주는 것이라고 해석할 수 있습니다. 왜 하나의 화면이어야 하는지는 SPA의 개념을 설명하면서 말씀드리겠습니다.

#### 1. SPA

리엑트는 단일 페이지로 구성되었습니다. 이 때문에 single page app이라는 SPA라고 불립니다. 또한 리엑트는 라이브러리이기 때문에 자체적으로 라우터를 가지고 있지 않습니다. 때문에 서드 파티 라이브러리에서 제공하는 라우터를 이용해야 합니다. 이 점이 프레임워크와 분리되는 지점이죠.

#### 2. Router

라우터 설치도 CRA처럼 npm을 통해 진행합니다.

```
npm install react-router-dom --save
```

위의 명령어를 리엑트 폴더에 입력하면 react-router-dom을 다운 받을 수 있습니다.

```jsx
import React from "react";
import { BrowserRouter as Router, Switch, Route } from "react-router-dom";

import Login from "./pages/Login/Login";
import Signup from "./pages/Signup/Sig nup";
import Main from "./pages/Main/Main";

class Routes extends React.Component {
  render() {
    return (
      <Router>
        <Nav />
        <Switch>
          <Route exact path="/" component={Login} />
          <Route exact path="/signup" component={Signup} />
          <Route exact path="/main" component={Main} />
        </Switch>
        <Footer />
      </Router>
    );
  }
}
export default Routes;
```

위의 컴포넌트가 라우터의 컴포넌트입니다. 상단의 import는 react-router-dom을 불러오는 용도입니다. BrowserRouter as Router라는 표현은 원래 BrowserRouter라고 써야하는 명령어를 Router로 줄여서 사용하겠다는 뜻입니다. 이렇게 줄인 명령어를 render 함수안에 <Router />로 이용하고 있는 것이 보입니다. 이 라우터 태그 내부에 있는 모든 파일들이 라우팅되는 것은 아닙니다. 그 내부의 <Route />내부 정보들만 교대로 페이지에 표기 됩니다. 지금은 3개의 페이지가 라우팅 중입니다. path를 통해 경로를 지정해주고, 각 컴포넌트 내부에 <Link>를 이용해 원하는 위치로 이동이 가능합니다. 링크와 함께 이동이 가능한 방법은 2가지인데요. 잠깐 설명을 드리겠습니다.

- link 컴포넌트 : react router dom에서 제공하는 컴포넌트임. a 태그는 페이지 세로고침, link는 새로고침 하지 않아서 리엑트의 SPA을 유지시켜줌

  ```
  <Link to="/main">여기를 눌러 페이지 이동</Link>
  ```

- this.props.history.push(): 이벤트나 필요 조건에 따라 이동을 하기 위해 사용하는 이동 함수. 주로 이벤트의 콜백 함수 내부에 위치함

  ```jsx
  import { withRouter } from "react-router-dom";

  goToMain = () => {
    this.props.history.push("/main");
  };

  <button className="loginBtn" onClick={this.goToMain}>
    로그인
  </button>;
  ```

#### 3. SASS

HTML과 바닐라 자바스크립트 정도를 다루면 CSS로 대부분 스타일 정리가 가능합니다. 그러나 프로그램의 규모가 커지면서 CSS로만으론 복잡함을 해결할 수 없었습니다. SASS는 CSS에 문법적인 요소를 추가해 중복을 피하고 그 자체로 구조적인 해석이 가능하도록 해준 기술입니다. 일반적인 CSS에 부모에서 자식이 {} 레벨로 묶인 것이라고 해석해도 좋습니다.

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
    li {
      display: inline-block;
    }
  }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

이렇게 nav란 부모 태그에 묶인 CSS의 구조를 명확히하고 서로의 스타일링을 뚜렷하게 구분해줍니다. 프로젝트가 커질 수록 에러와 실수를 줄여주는 고마운 기술입니다.
