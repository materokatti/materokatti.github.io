---
layout: single
title: "Svelte Store는 무엇일까?"
description: "Svelte Store에 대해 알아봅니다."
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0



---

 

#### Store는 무엇인가?

React에서 props를 전달하다보면 중간 전달자 위치의 컴포넌트는 자신은 사용하지도 않으면서 props를 불필요하게 전달하는 모습을 보여주기도 합니다. 이렇게 과도하게 중간 전달과정이 늘어나는것을 props 터널링이라고 부릅니다. 이런 터널링을 막고 필요한 데이터를 한 공간에서 끌어 쓰기 위한 방법이 store입니다.



#### Writable 함수

```
//store.js
import { writable } from 'svelte-store';
export const count = writable(0);
```

 writable은 가장 많이 쓰이는 store의 함수로 일고 쓰기가 가능합니다. `let count = writable(0)` 처럼 함수의 인자는 초기값을 지정하고, update를 사용해 현재값을 가져와 그와 비교해서 값을 수정합니다. set을 통해 현재값과 상관없이 값을 수정하죠.

```javascript
count.update(n => n+1);
count.set(100);
count.subscribe(value => countValue = value);
```

예시처럼 작성하면 잘 작동합니다. subscribe는 count 가 바뀔때 마다 작동하는 함수인데요. Count 값이 변화할 때 마다 콜백 함수를 불러오죠. 더 편리한 자동 구독 기능이 있는데요.

```javascript
$count = $count + 1;
$count = $count - 1;
```

이렇게 변수 앞에 $를 붙여주게되면 count값이 변환 할 때마다 값을 갱신해서 그려줍니다. 즉 굳이 update, subscribe 등을 통해 변화를 감지 할 필요가 없죠.



#### Readable 함수

 writable이 읽고 쓰는 기능이라면 readable은 사용자가 굳이 조작할 필요가 없는 값을 저장할 때 사용합니다.

```javascript
export const time = readable(new Data(), function (set){
	const interval = setInterval(() => {
		set(new Data());
	}, 1000)
	return function stop () {
		clearInterval(interval);
	}
})
```

 상단의 함수는 날짜 정보를 1초마다 사동 수정합니다. 자동으로 업데이트해서 날짜를 보여주는 경우 위처럼 readable의 첫 인자로 초기 값인 new Data()를 줍니다. 이후 function의 인자로 set을 설정하는데요. 이 set은 readable 함수 내부에서 setInterval에서 `set(new Data())`를 위해 활용됩니다.



#### Drived 함수

```javascript
const start = new Date();

export const elapsed = derived(
	time,   //참고할 store
	($time) => {
		return Math.round($time - start)
	}
)
```

drived 함수는 첫 인자로 참조할 스토어를 받고 그를 활용할 수 있도록 하는 함수입니다. 위 함수는 처음 들어온 시간을 start로 두고 시간이 지나가는 중인 time이란store를 첫 인자로 놓습니다. 그리고 `Math.round($time - start)`를 통해 현재 머문 시간을 보여주는 기능입니다.



추가적으로 custom store와 binding도 가능한 만큼 store를 활용할 수 있는 방법은 다양합니다. 이 역시 더 공부하고 싶어지게 만드는 주제네요.