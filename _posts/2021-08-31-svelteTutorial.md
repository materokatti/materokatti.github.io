---
layout: single
title: "Svelte.js Tutorial #1"
description: "Svelte.js 공식 홈페이지의 tutorial 입니다. #1"
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

#### Adding Data

 정적인 데이터 값을 넣는데는 HTML과 동일한 방식으로 작동합니다.

```html
<h1>Hello world!</h1>
```

이렇게 App.svelte에 입력해주면 Hello world가 출력되죠. 동적인 데이터 입력도 쉽습니다. script를 선언해주고 변수를 선언, JSX에 할당해주면 됩니다.

```react
<script>
	let name = 'world';
</script>

<h1>Hello {name}!</h1>
```

이렇게 동적인 데이터 입력도 가능합니다. 이걸 응용하면 image의 소스에도 사용 가능하죠.

```react
<script>
	let src = 'tutorial/image.gif';
</script>

<img src={src} alt='a man dances.' >
```

그러나 svelte의 경우 변수의 이름이 요구하는 값과 동일하다면

```react
<img {src} alt='a man dances.' >
```

이렇게 더 단순하게 표현이 가능합니다.



#### Styling

HTML처럼 svelte도 style tag를 삽입할 수 있습니다.

```html
<p>This is a paragraph.</p>

<style>
	p {
		text-align: center;
		font-size: 2rem;
		font-family: Arial;
	}
</style>
```

중요한 것은 이 스타일 태그의 scope는 전역이 아닌 컴포넌트 단위 scope라는 것이죠. 즉 외부의 p 값은 이 스타일링으로 영향을 받지 않습니다.

```html
<script>
	import Nested from './Nested.svelte'
</script>

<p>This is a paragraph.</p>
<Nested />

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

 위의 코드에서 Nested는 외부에서 추가한 컴포넌트입니다. 즉 이 컴포넌트는 하단의 스타일링에 영향을 받지 않습니다. Nested.svelte라는 파일 안에 직접 가진 style 태그로부터 스타일링 속성을 반영하는 것이죠.

또한 변수 내부에서 HTML을 선언해주는 도구도 제공합니다.

```
<script>
	let string = `this string contains some <strong>HTML!!!</strong>`;
</script>

<p>{@html string}</p>
```

이렇게 중괄호 내부에 @html을 넣어주면 값에서 html과 관련된 태그를 해석하고 출력해줍니다.



#### Reactivity

```html
<button on:click={incrementCount}>
```

이벤트를 부여하는 것도 :를 사용하는 점이 조금 차이를 보입니다.

```html
<script>
	let count = 0;

	function incrementCount() {
		count += 1;
	}
</script>

<button on:click={incrementCount}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>
```

그러나 전체적으로 보면 단순히 이 차이 뿐 아니라 state 선언을 굳이 하지 않아도 되는 등, 훨씬 간결한 코딩이 가능해지죠.



##### 반응형 선언

JS에는 반응형 선언이라는 표현은 없습니다. 그러나 Svelte에선 마치 반응하는 const 같은 개념으로 $:라는 선언을 하죠. React의 경우 랜더링시 선언을 다시하기 때문에 이럴 필요가 없습니다. 그러나 Svelte는 필요한 요소만 재할당해주는 구조로서 반응형 선언이 필요합니다.

```html
$: doubled = count * 2;

$: {
	console.log(`the count is ${count}`);
	alert(`I SAID THE COUNT IS ${count}`);
}

$: if (count >= 10) {
	alert(`count is dangerously high!`);
	count = 9;
}
```

이렇게 단순히 변수 선언을 넘어 함수, 가정문, console.log까지 반응형으로 구현이 가능합니다.



#### Props

 svelte도 다른 프레임워크와 마찬가지로 props를 전달할 수 있습니다. 이렇게 컴포넌트끼리 데이터 전달이 가능한 것이죠. 다만 컴포넌트를 넘겨주는 방식이 다른 라이브러리와 조금 차이가 있죠.

```html
<script>
	export let answer;
</script>
```

 이렇게 export로 컴포넌트를 받아옵니다. 조금 어색하죠. 전체 코드를 통해 보겠습니다.

```html
<script>
	import Nested from './Nested.svelte';
</script>

<Nested answer={42}/>
```

이렇게 부모 컴포넌트가 넘겨준 props를 

```html
<script>
	export let answer;
</script>

<p>The answer is {answer}</p>
```

자식이 export를 통해 받아옵니다. export라는 표현이 받아오는것에 직관적으로 맞지는 않지만 익숙해지면 햇갈리지 않는 개념입니다.

##### Default Value

```html
<script>
	export let answer = 'a mystery';
</script>
```

이런 식으로 지정도 가능합니다. 지정해줄 경우 props를 전달받지 못하는 경우 지정값이 props가 됩니다.



##### Spread Props

만약 객체 형태의 다양한 정보를 전달할 경우에는 

```html
<Info {...pkg}/>
```

이런식으로 펼쳐줄 수 있습니다.



#### Logic

##### 조건부 블록

HTML에서는 불가능하지만 스벨트는 조건부로 블록을 랜더링 할 수 있습니다. 

```html
{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
```

이처럼 단순한 if문 뿐 아니라 if else문을 통해서도 랜더링이 가능합니다.

##### each 블록

 react와 javascript에서 많이 사용하던 map 함수도 each로 전환이 가능합니다.

```html
{#each cats as cat, i}
	<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
		{i + 1}: {cat.name}
	</a></li>
{/each}
```

이렇게 전환하면 콜백 함수를 선언해줄 필요가 없기 때문에 매우 코드가 짧아집니다.

each 함수에서 key 값을 주는 방법은 아래와 같습니다.

```html
{#each things as thing (thing.id)}
	<Thing name={thing.name}/>
{/each}
```

스벨트에서 key값은 react보다 더 많은 역할을 합니다. 만약 맨 앞 부터 잘라 나가는 구성의 배열이나, 객체를 선언할 경우 참조 값으로 사용되기 때문이죠. 즉 key 값인 thing.id가 없다면, 변화가 반영되지 않는 오류가 생기곤 합니다. 말로 설명하면 어려우니 예시 링크를 첨부해 두겠습니다. (https://svelte.dev/tutorial/keyed-each-blocks)



##### Await block

```html
{#await myPromise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
```

데이터를 받아오는 결과에 따라 대기, 성공, 오류를 출력하는 경우도 이렇게 3단계로 나눠서 구성이 가능합니다. 조건부로 랜더링이 되기 때문에 직관적으로 조건에 따라 어떤 결과물이 나오는지 알아보기 쉽습니다. 조금 어려울 수 있어 해석을 하자면, myPromise가 Fetch API를 써서 정보를 받아오는 함수라고 가정하죠. 그렇다면 :then, :catch 뒤에 붙은 number와 error는 각각 응답이 성공했거나 실패했을때 데이터가 반환되는 값입니다.



#### Events

##### DOM events

```html
<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>
```

앞서 살펴보았듯 DOM을 조작하는 events는 on: 구조로 쓰면됩니다.



##### Inline handlers

 이벤트에 따른 내부 콜백 함수를 인라인으로 구성하면 따옴표를 붙여줍니다. 절대적인 규칙은 아니지만 강조를 위해 붙여주는 것이 관례이죠.

```html
<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>
```

 일부 프레임 워크에서는 inline 스타일의 이벤트를 피하라고 권장합니다. 그러나 svelte에서는 다른 프레임워크에서 나타나는 루프 문제 등이 없기 때문에 상관없습니다.
