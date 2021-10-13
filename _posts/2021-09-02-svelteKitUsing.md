---
layout: single
title: "SvelteKit 기본 활용법"
description: "Sveltekit의 기본적인 활용에 대해 알아봅니다"
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0


---

 저번 글에서 스벨트킷의 세팅과정을 말씀드렸죠 오늘은 스벨트 킷의 다양한 기능들을 가볍게 알아보겠습니다. 스벨트 킷은 최근 웹 개발에서 가장 흥미로운 프레임워크 중 하나입니다. Next.js(react 위체 구축 된 프레임 워크)와 Nuxt.js(Vue 기반)의 성공과 성장이 계속되는 가운데 SvelteKit은 가장 유망한 경쟁자입니다. Svelte킷을 사용하면 Svelte의 간결한 Syntax를 활용하면서 SSR, API 경로 등을 만들 수 있습니다.

#### 스벨트킷 시작

저번 시간에 세팅 과정에 대해 설명드렸지만 한 번 더 코드를 남기도록 하겠습니다.

```
npm init svelte@next my-app
cd my-app
npm install
npm run dev -- --open
```



#### 스타일링

세팅이 완료되면 `/src/routes/index.svelte` 에 기입된 정보가 화면에 나타날 겁니다. 그곳에 스타일을 적용해보겠습니다.

```html
//  /src/routes/index.svelte

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<style>
	h1 {
		color: red;
	}
</style>
```

이렇게 스타일링을 하면 이는 지역 변수로서 작용합니다. h1은 `class="s-Uap-jPRb-uiE"` 라는 클래스 값을 자동으로 할당 받는데요. 이런 방식으로 sveltekit에선 스타일링의 중복을 방지합니다.



####  svelte:head

스벨트 킷에서 html head에 들어가는 정보를 관리하는 독특한 문법이 있습니다. 바로 `svelte:head` 입니다. 이를 제외하고도 `option, self, window, body ` 등 다양한 요소를 : 뒤어 붙여서 구성이 가능합니다. head를 통해 title을 제어하는 예시를 보겠습니다.

```html
<svelte:head>
	<title>Svelte Kit</title>
</svelte:head>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
```

이런 식으로 index.svelte가 구성되었다고 하죠. 그러면 title 값은 Svelte Kit이 됩니다. 대부분은 웹 앱의 경우 타이틀 값이 전환되는 일은 없죠. 그러나 스벨트는 상황에 따라 마음대로 제어가 가능합니다. 

```html
<svelte:head>
	<title>CheckRouting.svelte</title>
</svelte:head>

<h1>Check Routing</h1>
<p>this is checking Routing</p>
```

이건 checkRouting.svelte라는 src/routes 폴더 내부의 파일입니다. 스벨트는 라우팅 기능을 기본 제공하기 때문에 이렇게 파일을 만들어도 로컬 포트에 /checkRouting 만 붙여주면 라우팅이 됩니다. 인상적인 점은 라우팅 된 타이틀이 CheckRouting.svelte로 바뀐다는 거죠. 상당히 독특한 구조입니다.



#### __layout.svelte

routes 폴더에 가면 레이아웃이라는 svelte 파일을 보실 수 있습니다.

```html
<!-- src/routes/__layout.svelte -->
<nav>
	<a href="/">Home</a>
	<a href="/about">About</a>
	<a href="/settings">Settings</a>
</nav>

<slot></slot>
```

처음 보면 뭔가 싶죠? 쉽게 말하면 React.js의 Routes.js 파일 처럼 변하는 요소와 변하지 않는 요소를 지정해주는 역할이라고 이해하시면 됩니다. 위 코드에선 변하는 요소는 `<slot>`입니다. 반면 상단의 `<nav>`는 고정되어있죠. 하단에 `<footer>`를 붙일 수도 있겠네요.

 혁신적인 요소는 이런 레이아웃 파일을 라우트 폴더마다 추가로 만들 수 있다는 겁니다. 기억해 둘 점은 이때는 `layout.reset.svelte`라는 이름으로 만들어줘야 합니다. Admin 페이지 같이 사용하던 레이아웃을 변화시키고 싶다면 사용 가능하죠.



#### load 함수

 페이지 또는 레이아웃을 정의하는 컴포넌트는 컴포넌트가 생성되기 전에 실행되는 로드 기능을 내보냅니다. 말이 어렵지만 쉽게는 컴포넌트가 그려지기 전 발생하는 함수라는 거죠. 독특한 점은 이 load는 클라이언트와 서버와 모두 통신합니다. React의 라이브러리인 Next.js에선 두 방식을 나눠놨지만 svelteKit은 load 하나로 통일됩니다.

```html
<script context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, fetch, session, context }) {
		const url = `/blog/${page.params.slug}.json`;
		const res = await fetch(url);

		if (res.ok) {
			return {
				props: {
					article: await res.json()
				}
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>
```

`<script context="module">`라고 붙어줘야만 load가 컴포넌트 생성 전 실행됩니다. 그 이외의 `script`요소는 아래에 새로 `script`태그를 다시 선언하고 안에 넣어줍니다. load는 페이지 접근, 패치, 또 가벼운 정보를 저장해두는 session 등의 역할이 있는데요. Fetch 할 때 page의 정보, 즉 url에 접근해 fetch 요소를 제어할 수 있는 등 유용한 역할을 합니다. 추가적으로 컴포넌트 생성 전에 발생하는 만큼 page 최상위 컴포넌트나 레이아웃에만 이용이 가능합니다. 즉 import 되는 컴포넌트는 load 함수를 쓸 수 없는 거죠.



#### $lib

React를 사용하다보면 ../../../ 같이 끝이 없이 빠져나가야 하는 구조들을 만나곤 합니다. 스벨트에선 이렇게 외부에서 붙어야 하는 파일들을 lib라는 폴더를 만들어 관리할 수 있습니다. src 폴더에 위치한 lib는 `$lib/`라고만 지정해주면 어디서든 lib로 접근이 가능합니다. 경로를 훨씬 단축시켜주죠.



#### Hooks

 훅은 리엑트의 함수형 컴포넌트를 보면 쉽게 접하는 개념입니다. 그러나 리엑트 훅은 리엑트의 함수형 구조를 완성하기 위한 독특한 요소입니다. 원래 프로그래밍의 개념에서 훅은 일정한 요소가 실행되면 뒤따라서 오는 요소들을 말합니다. 스벨트의 훅 개념은 후자이죠. 스벨트 훅은 `src/hooks.js`안에 담기는데 서버에 handle, handleError, getSession, externalFetch를 요청합니다.

```html
export async function handle({ request, resolve }) {
	request.locals.user = await getUserInformation(request.headers.cookie);

	const response = await resolve(request);

	return {
		...response,
		headers: {
			...response.headers,
			'x-custom-header': 'potato'
		}
	};
}
```

 handle을 예시로 보자면 발생 시점을 결정하는 request와 그 응답인 resolve를 인자로 받습니다. request는 처음 페이지가 그려지는 시점에 발생을 하는거죠.



오늘은 여기까지 하고 load 함수, hooks, 그리고 $app/stores 등 유용한 개념은 다음에 한 번 더 다뤄보도록 하겠습니다. 특히 props 터널링을 해결을 위해 존재하는 store에 대해서는 시간을 내어 자세히 다뤄볼 생각입니다. 