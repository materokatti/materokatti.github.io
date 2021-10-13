---
layout: single
title: "Sveltekit 시작 & tailwindcss 세팅"
description: "Sveltekit으로 웹 개발을 위한 세팅"
tags: [Svelte]
comments: true
published: true
categories: Svelte
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

 최근 스벨트에 대한 공부를 계속하고 있는데요. 오늘은 스벨트를 이용한 웹 개발 라이브러리인 스벨트 킷을 소개해보려고 합니다. 가벼운 소개 이후엔 시작하는 법을 간략하게 정리하겠습니다.

####  스벨트 킷이란?

 스벨트 킷은 스벨트의 플러그인과 Vite로 이뤄진 라이브러리입니다. 이들은 스벨트 언어가 가진 빠른 반응형 효과를 구현해 보다 혁신적인 UX 구현을 목적으로 합니다. 또한 최신 프레임워크, 라이브러리 들이 다양한 기능을 탑제하면서 복잡해진 것과 다르게 스벨트킷은 빠른 속도와 함께 직관적이고 단순한 구조를 제공합니다. 기능과 가독성을 모두 향상시키 좋은 경우죠. 유저의 경험 뿐 아니라 개발자에게도 좋은 점이 많습니다. 대표적인 것이 빠른 브라우저 전환입니다. 이로서 구성 요소가 바뀔 때마다 기다릴 필요가 없이 즉각적으로 전환하는 브라우저를 경험할 수 있죠.



#### 스벨트킷 시작하기

시작은 어렵지 않습니다.

```
npm init svelte@next my-app
cd my-app
npm install
npm run dev
```

위의 명령어를 순차적으로 실행하면 되는데요. 마치 React의 Create-react-app처럼 스벨트 킷을 통한 개발 환경이 세팅됩니다. 

`npm init svelte@next my-app` 명령어가 완료되면 뒤엔 다양한 세팅을 할 수 있습니다. Typescript, ESlint, Prettier등 설정이 가능합니다. 원하는데로 세팅을 하시면 스벨트 킷이 시작됩니다. 

 스벨트 킷은 빠른 속도 말고도 라우팅의 방식이 다른 점 등 기존 웹 개발 라이브러리와 다른 점을 보입니다. 이 차이점에 대해선 앞으로 차차 알아보도록 하죠. 



#### tailwindcss 세팅

 개인적으로 tailwindcss 세팅이 가장 어려웠습니다. tailwindcss의 공식 홈페이지에서 말한 방식으로 진행하면 다양한 오류들이 떴었죠. 그러다 svelte는 유저들에게 다양한 툴을 제공하기 위해 svelte-add를 만들었고 그곳에 tailwindcss가 포함되어있다는 글을 보았습니다. (사실 오늘 블로그 정리의 이유도 tailwindcss 세팅 과정에서 너무나 오래 어려움을 겪었기 때문입니다..)

```
npx svelte-add tailwindcss 
npm install
```

이렇게 npx로 tailwindcss를 깔아주면 루트 폴더에 postcss.config.cjs, tailwind.config.cjs 라는 두 파일이 생깁니다. 생긴 것을 확인 후에 `npm install` 을 해주면 tailwind를 위한 세팅이 마무리됩니다.