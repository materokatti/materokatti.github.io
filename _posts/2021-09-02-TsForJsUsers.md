---
layout: single
title: "Javascript 유저를 위한 Typescript"
description: "Typescript 공식문서 요약 #2"
tags: [TS]
comments: true
published: true
categories: TS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0


---



#### TS와 JS의 관계

TS는 JS 위에 레이어로서 자리잡고 있습니다. 또한 JS의 기능들을 제공하면서 그 위에 자체 레이어를 추가하죠. 이 레이어가 TS의 타입 시스템입니다. TS는 사용자가 생각한 일과 JS가 실제로 하는 일 사이의 불일치를 강조해줍니다.



#### 타입 정의하기

자바스크립트는 다양한 디자인 패턴을 가능하게 하는 동적 언어입니다. TypeScript는 TypeScript에게 타입이 무엇이 되어야 하는지 명시 가능한 기능을 제공합니다. 이 기능을 통해 JavaScript 언어의 확장을 지원하는거죠.

```javascript
const user = {
	name: 'Hayes',
	id: 0,
}
```

 이 객체를 타입스크립트를 통해 명시하면

```typescript
interface User = {
	name: string;
	id: number;
}
```

이렇게 나타 낼 수 있습니다. 형태를 명시적으로 나타내기 위해 interface로 선언합니다. 이 interface를 활용하려면

```typescript
const user: User = {
	name: 'Hayes',
	id: 0,
}
```

 이렇게 나타낼 수 있습니다. 선언된 인터페이스를 통해 클래스로 만들수도 있죠.

```typescript
interface User {
  name: string;
  id: number;
}

class UserAccount {
  name: string;
  id: number;

  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}

const user: User = new UserAccount("Murphy", 1);
```

또한 함수 뒤에 나타내어 매개변수와 리턴값의 형태를 명시하기도 합니다. 

#### 추가되는 데이터 타입

기존에 JS에서 사용되는 데이터 말고도 추가됨

interface를 우선 사용하고 특정 기능이 필요할 때 type 사용

#### 타입 구성

여러가지 타입을 이용해서 새 타입을 만드는 방법들이 있습니다. 가장 많이 사용되는 두 가지는 유니언과 제네릭입니다. 

##### 유니언

유니언은 타입이 여러 타입 중 하나일 수 있음을 선언하는 방법입니다. 예를 들어

```typescript
type MyBool = true | false;
```

이런 형태로 불리안 값의 타입을 지정 할 수 있습니다. 또한

```typescript
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

 이렇게 허용되는 스트링 값 또는 number 값을 지정할 수 있죠. 조금 심화로 넘어가면

```typescript
function wrapInArray(obj: string | string[]) {
  if (typeof obj === "string") {
    return [obj];
//          ^?
  } else {
    return obj;
  }
}
```

이렇게 들어오는 값을 string과 배열로 나누고 그에 따른 조건문 활용도 가능합니다. 

##### 제네릭

 제네릭에 대해 간단히 알아보자면 타입에 변수를 제공하는 방법이라고 할 수 있습니다. 

```typescript
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;	
```

  배열이 가장 일반적인 예시인데요. 이렇게 배열에 값을 지정해주고나면 조건에 맞는 배열만 들어올 수 있습니다.



#### 구조적 타입 시스템

구조적 타입 시스템은 두 객체가 같은 형태를 가지면 같은 것으로 간주하는 것입니다. 예시를 통해 보죠.

```typescript
interface Point {
  x: number;
  y: number;
}

function printPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}

// "12, 26"를 출력합니다
const point = { x: 12, y: 26 };
printPoint(point);
```

위의 point 변수는 Point 타입으로 선언된 적은 없지만 타입 검사를 통과합니다. 즉 둘 다 같은 형태의 타입이기만 하면 선언과 상관없이 타입 테스트를 통과할 수 있습니다. 

```typescript
// @errors: 2345
interface Point {
  x: number;
  y: number;
}

function printPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}
// ---cut---
class VirtualPoint {
  x: number;
  y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}

const newVPoint = new VirtualPoint(13, 56);
printPoint(newVPoint); // prints "13, 56"
```

이 점은 클래스와 객체가 형태를 따르는 방법에 차이가 없는 부분으로 연결됩니다. 객체 또는 클래스 역시 필요한 모든 속성만 존재한다면 구현 세부 정보와 관계없이 일치하다고 봅니다.

