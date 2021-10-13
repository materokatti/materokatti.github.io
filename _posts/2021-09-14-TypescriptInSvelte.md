---
layout: single
title: "vscode에서 타입스크립트로 인한 경고 지우기"
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

 저번 시간에 이어 오늘은 실질적으로 TS를 활용한 Sveltekit 개발 방법에 대해 알아봅니다. 저번 시간에 말한 방법으로 타입 스크립트를 쓰게 될 경우 VScode 등 에디터에서 타입 설정이 되지 않은 변수들은 경고 메시지를 보냅니다.

```html
<script lang="ts">
	import { page } from '$app/stores';
	export let buttonName = [];
	export let link: string;
	export let svgPathD;
</script>
```

예를 들어 위의 경우 let으로 선언된 buttonName의 경우 타입 설정이 없습니다. 지금은 괜찮지만 나중에 내부의 요소를 사용하게 된다면 그 요소를에 '빨간줄'을 그어서 타입 설정이 되지 않은 값이라고 알려줍니다. 때문에 타입 설정은 습관적으로 해두도록 해야 하죠. 

	import { page } from '$app/stores';
	export let buttonName: array<any> = [];
	export let link: string;
	export let svgPathD: any;

만약 단순히 빨간 줄을 피하고 싶다면, 이렇게 any 나 object 타입을 선언하면 해결이 됩니다. any는 어떤 값이든 들어가도 되기 때문이고 object 역시 JS 최상위 데이터 타입이라 비슷한 효과를 가져옵니다. 그러나 이는 급한 불 끄는 것에 불과하구요. 최선은 변수, 함수를 선언할 때 마다 올바른 타입을 설정해두는 것이 옳은 방법이죠.