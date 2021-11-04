---
layout: single
title: "프로토타입 기본 개념 이해하기"
description: "JS 프로토타입의 기본정보를 알아봅니다"
tags: [Javascript]
comments: true
published: true
categories: Javascript
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

자바스크립트는 프로토타입 기반의 언어입니다. 클래스 기반언어는 상속을 사용합니다. 그러나 프로토타입 기반의 언어는 어떤 객체를 원형(prototype)으로삼고 이를 복제 함으로써 상속과 비슷한 효과를 가져옵니다. 다수의 유명한 언어들이 클래스 기반이지만 JS는 프로토타입을 기반으로 삼아 그들과 차별점을 보이는게 특징이죠. 오늘은 이 프로토타입에 대해 알아봅니다. 그럼 예시코드와 함께 기본 개념부터 알아보겠습니다

## Constructor, Prototype, Instance

프로토타입의 가장 기본개념은 constructor, protorype, instance 라는 세 가지입니다.

```jsx
var instance = new Constructor();
```

위의 코드처럼 변수가 선언되었다고 하죠. 이렇게 new 연산자를 통해 생성자 함수(constructor)를 호출하면 이 생성자 함수를 바탕으로 새로운 instance가 생성됩니다. 그리고 이 instance에는 '__proto__' 라는 프로퍼티가 자동으로 부여되는데 이 프로퍼티는 Constructor의 prototype이라는 프로퍼티를 참조합니다.

생소한 개념들이 한꺼번에 등장해서 어수선하죠? 정리를 하겠습니다.

- Constructor : 생성자 함수로 프로토타입을 복제한 새로운 요소를 만들어준다.
- Instance: 생성자 함수를 통해 만들어진 복제본을 Instance라고 한다.
- Prototype: 복사가 되기 전 원형 프로토타입의 소속 객체로 복사한 인스턴스가 사용한 메서드를 저장한다.
- '__proto__': prototype 객체의 복사본으로 인스턴스는 이것을 통해 사용할 메서드에 접근한다.

이 정도로 정리가 될 수 있습니다. 어느정도 이해에 도움이 되셨나요?

```jsx
주의!!
편의를 위해 __proto__라는 표현을 계속 사용하지만,
이는 브라우저에서 편의를 위해 prototype에 접근하는 방식입니다. 
실무에서는 가급적 Object.getPrototypeOf()/Object.create()등을
이용해야 합니다.
```

한 가지 주의해야 할 점을 추가하자면 

```jsx
var Person = function(name){
	this._name = name;
}

Person.prototype.getName = function() {
	return this._name;
}

var human = new Person('James')
human.__proto__.getName(); // undefined
```

이런 코드의 경우 `human.__proto__.getName()` 처럼 proto를 붙여주면 this가 원하는 위치에 바인딩 하지 못합니다. 즉 본인이 소속된 객체에 바인딩되는 this의 특성상 `__protp__` 를 this로 지정하고 거기에 name이 없기 때문에  `undefined` 이 출력된 겁니다. 이 경우

```jsx
human.getName(); // 'James'
```

위 코드 처럼 `__proto__` 를 제거 해주면 인스턴스를 this로 지정하게 됩니다. 이게 가능한 이유는 proto 객체는 생략이 가능하기 때문입니다. 이 객체는 애초에 생략이 가능하도록 설계 구조상 설정되어있습니다. 때문에 이해의 영역이라기 보다는 그냥 받아들이는 것이 편하죠. 이런 생략 덕분에 `prototype` 객체를 통해 전달받은 메서드는 마치 인스턴스가 가지고 있는 메서드 처럼  `__proto__` 없이 선언이 가능합니다. 

```jsx
var arr = [1, 2]
arr.map(function(){})     // arr.__proto__.map(function(){})
arr.forEach(function(){}) // arr.__proto__.forEach(function(){})
```

 위처럼 우리가 기본적으로 알고있는 배열 메서드 역시 prototype을 통해 생성자 함수로부터 전달받은 것이죠. 때문에 앞서 말했듯 `__proto__` 를 생략하고 바로 메서드를 선언해도 올바르게 작동합니다.

 

## 프로토타입 체인

 프로토타입 체인은  `__proto__` 프로퍼티 내부에  `__proto__` 프로퍼티가 연쇄적으로 이어진 것을 의미합니다. 이게 어떻게 가능할까요? 코드를 보죠.

```jsx
var arr = [1, 2]
arr(.__proto__).push(3);
arr(.__proto__)(.__proto__).hasOwnProperty(2); // true 
```

이렇게 생략과정이 두번으로 연쇄적인 연결이 가능합니다. 두번째  `__proto__` 는 어떤 prototype일까요? 바로arr 배열의 prototype 스스로가 객체이기 때문에 객체로서의 `__proto__` 를 가지는 것입니다. 즉 두번째 `__proto__` 에는 객체가 가지는 메서드가 들어있는 것이죠. 이렇게 연결된 prototype의 구조를 프로토타입 체인이라고 부릅니다. 프로토타입 체이닝은 메서드 오버라이드와 동일한 원리로 동작합니다. 잠시 메서드 오버라이드를 알아보자면,

```jsx
var Person = function (name) {
	this.name = name
};
Person.prototype.getName = function () {
	return this.name
};

var james = new Person('James');
james.getName = function(){
	return 'hey!' + this.name;
}
console.log(james.getName()); // hey! James
```

위의 코드처럼 원래 있던 메서드의 위치에 인스턴스가 메서드를 더하면 작동합니다. prototype으로 전달된 메서드가 없어지는 것은 아닙니다. 다만 가장 먼저 인스턴스가 메서드를 가지고 있는지 판단하고, 없다면 prototype단으로 넘어가는 것이죠. 이러한 순차적인 작동은 프로토타입 체인에서도 동일하게 작동합니다. 첫 arr 의 프로토타입에서 없다면, 다음인 객체의 prototype으로 넘어가는 것이죠.

 위 코드에서 Person의 prototype은 객체의 프로토타입을 부여받습니다. 만약 여기서 배열이 가지고 있는 프로토타입으로 변경시켜주고 싶다면 어떻게 하면 될까요? 간단합니다.

```jsx
Person.prototype = [];
```

 이 코드 한 줄이면 생성자 함수인 Person의 프로토타입은 객체의 그것을 따르게 됩니다. 이렇게 프로토타입 체인은 변경 역시 가능하다는 점 알아두며 이번 시간은 마치겠습니다.