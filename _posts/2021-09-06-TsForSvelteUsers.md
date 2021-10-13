---
layout: single
title: "Svelte + Typescript"
description: "Typescript for svelte"
tags: [TS]
comments: true
published: true
categories: TS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0




---

2020년 중순까지만 해도 svelte에 타입스크립트 적용이 불가능했습니다. 당시 추가에 대한 요구가 지속되자 svelte는 typescript를 도입 했죠.

#### SvelteKit에 Typescript 설치

 svelte만 사용할 경우 npm을 통해 typescript를 가져와야 하지만 svelteKit에서는 기본적으로 typescript를 제공합니다. 처음 설치하는 과정에 `npm init svelte@next my-app` 을 실행하면 데모 버젼 혹은 Skelton 버젼을 선택하라고 나오고, 이후 typescript 설치에 대한 안내가 나옵니다. 이용하겠다는 yes를 선택하면 typescript 활용이 가능합니다. 



#### 컴포넌트에 적용

이후엔 따로 import 해줄 필요는 없습니다. 

```html
<script lang="ts">
	import { page } from '$app/stores';
	export let buttonName;
	export let link: string;
	export let svgPathD;
</script>
```

위와 같은 방식으로 `<script>` 뒤에 lang='ts'라는 방식으로 타입 스크립트를 선택해주고 변수, interface 등을 선언해주면 됩니다.



#### 값 확인

 값 확인을 위한 과정은 `npm run svelte-check` 라는 명령어로 가능합니다. 조금 길기 때문에 저는 커스터마이징을 활용하는데요.

```json
"scripts": {
		//...scripts
		"validate": "svelte-check"
	},
```

 Config.js에 위 처럼 명령어를 설정해주고 `npm run validate` 라는 명령으로 대체하면 됩니다. 

 이게 전부입니다. svelteKit에서는 이미 제공해주는 기능이기 때문에 추가적인 세팅이 필요없습니다. 유용하게 쓰이길 바랍니다 :)