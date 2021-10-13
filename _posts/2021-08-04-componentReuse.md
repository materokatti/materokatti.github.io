---
layout: single
title: "component 재사용에 관하여"
description: "component, reuse??"
tags: [React]
comments: true
published: true
categories: React
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

 안녕하세요 오늘은 React의 컴포넌트 재사용에 관하여 간략하게 이야기 해 보려고 합니다. 컴포넌트 재사용을 위해 어떤 점을 염두해야 하는지를 기준으로 이야기 해보도록 하죠.

#### 1. 화면을 보고 구성 요소 나누기

 먼저 화면에서 반복적으로 사용이 가능한 요소들을 찾아야 합니다. 변화하는 부분이 있으면 이를 props 형식으로 전달해주는 방식이 가장 간단한 컴포넌트 재사용이죠. 공통의 요소를 고정시켜두고 변화 지점만 props로 전달해줍니다. 이것만 지켜줘도 굉장히 경제적인 react 활용이 가능합니다.

#### 2. 하위 컴포넌트로 내려줘야 할 데이터 구조 결정하기

 요소를 구분했다면 이제 어떻게 props로 연결해줄지 고민해야 합니다. 상위 컴포넌트에서 하위 컴포넌트가 받아야 할 정보를 제공해주는데요. 텍스트 등 직접적으로 표현되는 정보 뿐 아니라, 표현해야 할 컨텐츠가 있을 경우 있다, 혹은 없을 경우 없음 을 알려주는 boolean 성격의 정보도 가능합니다. 즉 일정 조건을 만족하는 컴포넌트에는 다른 컴포넌트와 다른 UI를 보여주고 싶을때 이런 타입의 유무 형식으로 제어가 가능한 것이죠.

#### 3. this.props.children 

 this.props.children란 개념을 아시나요? 깊게 react를 배우지 않은 제겐 생소한 개념이었습니다. 그러나 활용 가능성이 다양한 굉장히 유용한 기능이라고 생각됩니다. 쉽게 말하면 props의 테그 안쪽에 다양한 형태의 정보를 넣어 이를 children 이란 props로 재활용 하는 것이죠. 예시를 하나 보여드리겠습니다. 

```react
export default class Form extends Component {
  render() {
    const { type, title, inputData } = this.props;

    return (
      <FormLayout>
        <h2>{title}</h2>
        <div>
          {inputData.map((input, idx) => (
            <Input
              key={idx}
              type={input.type}
              text={input.text}
            />
          ))}
        </div>
        <Button value={title} />
        {type === "signUp" && (
          <p className="isAlreadyLogin">
            이미 가입하셨나요? <span>로그인</span>
          </p>
        )}
      </FormLayout>
    );
  }
}
```

 이렇게 formLayout이란 컴포넌트 내부에 jsx를 넣은 것이 대표적인 사례죠. 이 경우 FormLayout에서 this.props.children이라고 저 jsx를 받아올 수 있습니다. 컴포넌트에 단순 정보 뿐 아니라 jsx, 함수 등 다양한 형태를 전달할 수 있는 좋은 기능입니다.