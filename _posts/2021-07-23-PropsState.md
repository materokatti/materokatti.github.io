---
layout: single
title: "Props, State?"
description: "Props, State, Event??"
tags: [React]
comments: true
published: true
categories: React
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요 오늘은 리엑트의 주요 개념 중 props, state 그리고 event에 대한 개괄적인 이해를 해보는 시간입니다.

#### 1. Props?

props는 쉽게 말해 부모 컴포넌트가 자식에게 전달하는 정보입니다.

```jsx
<Header name="Smith" age="24" />
```

Header라는 컴포넌트가 있다고 할 때, 그 부모 단에서 전달하는 name과 age를 props라고 할 수 있습니다. 모든 컴포넌트가 기본적으로 가지고 있으며 객체의 형태입니다. 단순 정보부터 함수까지 전달이 가능합니다. 특징이 있다면 부모에서 자식에게 전달하는 방향을 가질 뿐 자식 단에서 이를 변경할 방법은 없습니다.

#### 2. State

말 그대로 상태를 의미합니다. Property 즉 props와 다르게 모든 컴포넌트가 각각의 상태를 가질 수 있으며 state를 가진 요소 스스로 이를 조절할 수 있습니다. props 만큼 종속적인 조건은 아닌 것이죠. 그럼에도 리엑트는 부모에서 자식으로 내려오는 정보의 방향을 유지해야 합니다. 이러한 단방향성이 안정적인 소통을 가능하도록 하기 때문입니다. 이 때문에 state 값 역시 props처럼 상위 부모 컴포넌트에서 선언하고 이벤트를 이용해 자식 단에서 통제하는 방향을 유지해야 합니다. 이를 state 끌어올리기라고 합니다.

```jsx
constructor() {
    super();
    this.state = {
      value: '',
      commentList: [],
    };
  }
```

모든 state는 constructor를 통해 선언됩니다. 함수형에서는 좀 다르지만 우리는 state 개념을 이해하기 쉬운 class형으로 다루겠습니다. Super()를 통해 상태를 초기화해주며, this.state의 기본값을 설정해줍니다. 이렇게 state사용을 위한 초기 설정은 마무리됩니다. 초기 설정이 마무리되면 State를 변화시키는 방법을 배워야 합니다. 고정된 state는 의미가 없습니다. 그 변화를 통해 UI를 제어하는 것이 state의 목적이기 때문이죠. 그럼 이를 변화시켜보죠.

```jsx
getValue = (e) => {
  this.setState({
    value: e.target.value,
  });
};
```

위 함수는 한 이벤트의 콜백함수입니다. 내부에 setState라는 함수가 실행된 것을 볼 수 있습니다. state에 대한 변경은 setState 함수를 통해서만 가능합니다. 아니 엄밀히 말하면 아래와 같은 형태로도 변경이 가능하긴 합니다.

```jsx
this.State.value = e.target.value;
```

그러나 이 경우엔 state값이 변경 되었다는 것을 리엑트가 인지하지 못합니다. 그래서 render()를 실행시키지 않습니다. 리엑트가 SPA를 구현하기 위해서, 또한 state값의 변화에 따라 유동적인 UI를 구성하기 위해서는 rendering이 생명인데 이것이 불가능한 것이죠. 의미 없는 변수의 전환일 뿐입니다. 꼭 setState를 사용해야만 하는 이유입니다.

또한 부모 컴포넌트에서 state 선언시 부모 수준에서 함수를 만들어줘야합니다. 자식단에서 함수가 선언되면 setState가 자식의 state를 변경시키기 때문에 원하는 대상을 변경하는 것이 불가능합니다. 부모에서 state와 함수 모두 넘겨줘야 합니다.

#### 3. 예시

이제 오늘 배운 props와 state를 이벤트와 함께 코드로 살펴보겠습니다.

```jsx
  constructor() {
    super();
    this.state = {
      value: '',
      commentList: [],
    };
  }

  getValue = e => {
    this.setState({
      value: e.target.value,
    });
  };

  addComment = () => {
    if (!this.state.value) {
      alert('add comment pls');
    } else {
      this.setState({
        commentList: this.state.commentList.concat([this.state.value]),
        value: '',
      });
      document.getElementsByClassName('commentInput')[0].value = '';
    }
  };
```

위 코드는 제가 구현한 댓글 기능입니다. render부분을 제외한 class의 상단인데요. constructor로 state를 초기화해주고 getValue 함수를 통해 setState 해 주는 모습을 볼 수 있습니다. 그 하단의 addComment 함수는 가져온 value 값을 commentList라는 state의 배열에 저장하는 함수죠. 중간에 concat 매서드를 이용해 배열을 연장해 주는 것을 볼 수 있습니다. 이제 이렇게 연장한 배열들이 JSX에서 어떻게 확장되는지 보시죠.

```jsx
  render() {
    return (
      <>
          <div className="commentLine">
            <ul>
              {this.state.commentList.map((comm, idx) => {
                return <Comment key={idx} msg={comm} />;
              })}
            </ul>
          </div>
          <div className="articleComment">
            <i className="far fa-smile"></i>
            <input
              className="commentInput"
              type="text"
              placeholder="add a comment.."
              onChange={this.getValue}
            />
            <button onClick={this.addComment}>
              <i className="fas fa-check"></i>
            </button>
          </div>
      </>
    );
   }
```

먼저 인풋과 버튼에 이벤트를 설정해줍니다. 각 이벤트는 getValue와 addComment를 가지며 state변경과 댓글 업로드를 하고 있습니다. 댓글이 업로드 되는 위치는 <ul>의 하단에 있습니다. 조금 더 자세히 볼까요?

```jsx
<ul>
  {this.state.commentList.map((comm, idx) => {
    return <Comment key={idx} msg={comm} />;
  })}
</ul>
```

JSX이기 때문에 중괄호에 들어가 있습니다. 내부에 map 함수를 선언해서 각 배열을 <Comment />란 컴포넌트 형식으로 펼치고 있습니다. Comment는 제가 만든 댓글 컴포넌트입니다. 내부에 값을 comm이란 형식으로 받고 있고 key 값으로 인덱스를 취하고 있는 모습이 보입니다. 그런데 key 값은 왜 넣었을까요?

#### 4. 고유한 Key 값이 필요한 이유

리엑트에서 배열을 요소로 전환하면 고유한 키 값을 요구합니다. 사실 꼭 필요한 요소는 아닙니다. 그러나 엘리먼트에 고유성을 부여하고 안정적인 지정, 삭제, 확인을 위해 값을 넣는 것을 권고하는 것이죠. 가장 베스트는 배열 안에서 분류 가능한 요소를 부여하는 것입니다. 인덱스는 사실 최후의 수단이죠. 순서가 섞일 가능성이 있는 인덱스 값은 고유한 키 값으로 좋지는 않죠. 하지만 선택권이 없다면 리엑트 내부에서 인덱스를 키 값으로 선언합니다. 키 값은 부모 하위의 자식 단에서는 동일한 키를 사용해도 좋습니다. 한 컴포넌트 내에서 충동만 없다면 관대한 조건을 가지고 있는 것이죠.
