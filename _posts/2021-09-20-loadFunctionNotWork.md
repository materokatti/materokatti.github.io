---
layout: single
title: "SvelteKit load function localstorage 접근 오류"
description: "SvelteKit의 load function에 대해 알아봅니다."
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0




---

 Load function은 컴포넌트가 그려지기 전에 제한된 작업을 진행할 수 있게 하는 sveltekit의 기능입니다. 이 제한된 작업에는 page, session 접근, 그리고 fetch 등이 있습니다. 

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

 공식문서에 담긴 모습은 이렇게 되어있죠. 상단 load 우측으로 page, fetch, session, context 4가지를 조합해 원하는 세팅을 해 줄 수 있습니다. 특히 필요한 패치는 conponent 완성 전에 불러올 수 있다는 점은 유용합니다. 



## 로컬스토리지 접근 불가 오류

 제가 경험한 오류는 로컬 스토리지 접근 불가 였습니다. 전 컴포넌트 전에 패치를 진행해 끊김없이 빠르게 정보를 가져오려고 했죠. 그러나 fetch 단계에서는 브라우저단에서 실행되는 개념이 아닙니다. 때문에 localstorage, alert등 다양한 브라우저 제공 함수를 사용할 수 없죠. 

 이 문제 해결을 위해 어쩔 수 없이 onMount 함수로 컴포넌트가 생성되는 시점에서 정보를 받아왔습니다. 결과적으로 해결했지만, 문제는 데이터 로딩 중 끊김이 발생하는 것이었죠. 끊김 해결을 위해 spinner 같은 눈속임을 사용해서 어찌어찌 마무리 했죠. 하지만 다음부턴 localstorage 이외의 요소에 토큰을 저장하거나 fetch 단에 로컬 스토리지 접근이 필요 없는 방식으로 문제를 해결해야 겠습니다.