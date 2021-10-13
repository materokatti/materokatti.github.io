---
layout: single
title: "Svelte.js Tutorial #2"
description: "Svelte.js 공식 홈페이지의 tutorial 입니다. #2"
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

#### Event

##### Event modifiers

스벨트는 이벤트 작동을 조작하는 modifier를 제공합니다. 

```html
<script>
	function handleClick() {
		alert('no more alerts')
	}
</script>

<button on:click|once={handleClick}>
	Click me
</button>
```

예를 들어 위 이벤트는 단 한번만 작동하죠. 이 뿐 아니라 `preventDefault` ,` stopPropagation`, `passive`, `nonepassive`, `capture`, `self`, 등등 다양한 이벤트 제어자가 존재합니다. 연습해볼 가치가 있겠네요 :) (참고로 `on:click|once|capture={...}` 처럼 연결도 가능합니다.)



##### Component event (dispatch)

 스벨트는 데이터 뿐 아니라 이벤트도 전달할 수 있습니다. 이 전달과정은 자식에서 부로의 방향으로만 일어납니다. 

```html
<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>

<button on:click={sayHello}>
	Click to say hello
</button>
```

 먼저 이런 형태로 dispatch를 사용할 수 있는 조건을 만들어줍니다. 이 세팅이 되면 부모로 이벤트 전달이 가능합니다. `dispatch('message', {text: 'Hello!'});` 에서 첫 인자인 message가 전달할 이벤트의 명칭입니다. 두 번째 인자인 객체는 이벤트를 통해 전달할 detail 값이죠. detail은 다음 코드와 함께 알아보겠습니다.

```html
<script>
	import Inner from './Inner.svelte';

	function handleMessage(event) {
		alert(event.detail.text);
	}
</script>

<Inner on:message={handleMessage}/>
```

이런 식으로 Inner로 import해 온 경우 React에서는 이벤트를 붙일 수 없습니다. 그러나 스벨트는 자식으로부터 전달해 마치 이벤트를 가진 것 처럼 흉내낼 수 있습니다. 앞서 이벤트 이름으로 정한 message를 `on:message` 형식으로 써 줍니다. 그리고 콜백 내부에 `event.detail` 이 보입니다. 여기가 두번째 인자인 객체의 자리입니다. 이런 식으로 구성하면 객체의 키 값인 text를 다이나믹하게 변화시켜 서로 다른 이벤트를 보여줄 수 도 있을 겁니다. 마찬가지로 연습할 가치가 넘치는 기능입니다 :)



##### Event forwarding

컴포넌트 단에서 이벤트 전달이 가능하기 때문에 중간에서 다리 역할을 해 줘야 하는 경우도 생깁니다. 이럴 때 원칙상 중간에도 dispatch를 한 번 해줘야 합니다.

```html
<script>
	import Inner from './Inner.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function forward(event) {
		dispatch('message', event.detail);
	}
</script>

<Inner on:message={forward}/>
```

즉 이 구조로 evant.detail 값부터 'message'라는 이벤트 명칭까지 전달하는 거죠. 그러나 이러면 코드가 과도하게 비대해집니다. 그래서 스벨트는 단순한 방법을 만들었습니다.

```html
<script>
	import Inner from './Inner.svelte';
</script>

<Inner on:message/>
```

이 코드는 위와 동일한 역할을 합니다. 아주 간결해졌죠.



##### DOM event forwarding

DOM event도 forwarding이 가능합니다.

```html
<script>
	import CustomButton from './CustomButton.svelte';

	function handleClick() {
		alert('Button Clicked');
	}
</script>

<CustomButton on:click={handleClick}/>
```

 이렇게만 쓰면 `CustomButton` 이 import된 요소이기 때문에 이벤트를 받지 못합니다. 

```html
// ./CustomButton.svelte

<button on:click>
	Click me
</button>
```

 그래서 import 하는 컴포넌트에 on:click만 붙여주면 간단하게 연결 할 수 있죠.



#### Bindings

스벨트의 데이터는 하향식으로 아래로 전달되는 것이 기본입니다. 그러나 가끔 데이터를 위로 전달하는 방식이 필요하기도 하죠. React에서는 인풋 값에 따라 값을 변하게 해주려면 이벤트를 설정해 e.target.value 값을 만들어 state에 넣어 전달했습니다. 굉장히 번거롭죠. 스벨트에서는 bind 하나로 전달과정을 단순화 할 수 있습니다.

```html
<input bind:value={name}>
```

이렇게 하면 name 변수의 값은 입력값과 연동됩니다. 단순하죠. 숫자도 마찬가지입니다.

```html
<script>
	let a = 1;
</script>

<input type=number bind:value={a} min=0 max=10>
<input type=range bind:value={a} min=0 max=10>
```

이렇게 쉽게 연동이 되죠.

```html
<input type=checkbox bind:checked={yes}>
```

체크 박스의 경우 value 값이 없고 대신 `bind:checked` 를 활용합니다.

```html
<input type=checkbox bind:checked={yes}>
```

라디오 인풋이나 두개 이상의 체크박스는 group으로 묶어서 bind할 수도 있습니다.

```html
<input type=radio bind:group={scoops} name="scoops" value={1}>

{#each menu as flavour}
	<label>
		<input type=checkbox bind:group={flavours} name="flavours" value={flavour}>
		{flavour}
	</label>
{/each}
```

value라는 변수를 사용하면 보다 더 간결하게 쓸 수 있는데요.

```html
<script>
let value = `Some words are *italic*, some are **bold**`;
</script>

<textarea bind:value={value}></textarea>
```

원래는 이렇게 써줘야 맞지만, 

```html
<textarea bind:value></textarea>
```

이렇게 써도 동일하게 작동합니다. 이건 text area 뿐 아니라 모든 bind에 동일하게 작동합니다.



##### Contenteditable bindings

내용 편집 즉 `constenteditable='ture'` 일 경우 innderHTML을 수정하도록 binding이 가능합니다. 

```html
<script>
	let html = '<p>Write some text!</p>';
</script>

<div
	contenteditable="true"
	bind:innerHTML={html}
></div>
```

이렇게 하면 내부에는 아무 것도 없지만, html에 할당된 p 태그를 읽어서 표현하게 됩니다. 



##### Each block bindings

 #each에 대해서 bind를 추가할 수도 있습니다.

```html
{#each todos as todo}
	<input
		type=checkbox
		bind:checked={todo.done}
	>

	<input
		placeholder="What needs to be done?"
		bind:value={todo.text}
	>
{/each}
```

그러나 이 경우 배열과 상호 작용을 할 때마다 배열 내부의 값이 변할 수 있기 때문에 주의해야 합니다. 만약 변화가 불가능한 배열로 작업해야 한다면 이벤트 핸들러를 사용하는게 더 적절하죠.
