---
layout: single
title: "RESTful API에 대해"
description: "RESTful API란??"
tags: [WEB]
comments: true
published: true
categories: WEB
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0



---

  RESTful API는 무엇일까요?



#### API 시스템 구현을 위한 아키텍쳐중 가장 널리 사용 되는 것

API 시스템의 아키텍쳐는 다양합니다. Graphql, GRPC, REST 등이 있습니다. RESTful API는 이 중에서 REST 형식의 아키텍쳐인 것이죠. 



#### semantic code 같은 느낌으로 알아보기 쉽게 쓴 api 코드

 한 마디로 말하면 알아보기 쉬운 api의 형식라 할 수도 있습니다. URL 중에서 URI는 뒷 부분으로 해당 데이터가 위치한 곳을 명시하는 주소입니다. 즉 URL에서 도메인과 프로토콜을 땐 뒷 부분을 말하는 것이죠. RESTful API는 이 URI 부분을 직관적으로 알아보기 쉬운 방식으로 작성하는 것을 말합니다. http 메서드를 통해 Payload 즉 데이터를 전달받게 되는데, 이 전달을 효과적으로 이해하기 위해 고안된 것이죠. 



#### URI는 /를 통해 종속관계를 구분

product/category/01 등으로 /를 통해 종속을 구분합니다. 한 가지 주의할 점은 종속관계를 명확히 하기 위해서 맨 마지막에 /를 붙여선 안된다는 것이죠. 



#### URI는 페이지 별로 만드는 것 보다 기능별로 나누는 게 원칙

 페이지 별로 URI를 나누게 되면 같은 용도의 데이터가 페이지별로 나뉘게 됩니다. 이는 데이터 간의 종속관계를 명확히 하는 것을 방해하고 재사용도 불편해집니다. 때문에 기능 별로 나누는 것이 원칙이죠. 

