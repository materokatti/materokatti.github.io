---
layout: single
title: "React.js에서 Google map api 사용하기"
description: "React.js에서 Google map api 사용법 알아보기"
tags: [React]
comments: true
published: true
categories: React
sitemap:
  changefreq: daily
  priority: 1.0
---

안녕하세요. 오늘은 Google Map에서 제공하는 Api를 이용해 React.js에서 지도를 구현하는 방법을 알아보겠습니다. 지도를 어플에서 구현하면 정말 다양한 활용이 가능합니다. 일단 오늘은 React에 Google Map api 정보를 가져오는 정도만 알려드리도록 하겠습니다.

https://github.com/google-map-react/google-map-react

상단의 주소에 접속하면 Google-map-react라는 깃허브 레파지토리로 연결됩니다. 이곳을 통해 우리는 react에 지도효과를 적용할 수 있는 것이죠. 다운로드는 단순합니다. 주소 하단에 더 상세한 설명이 나와 있지만 그래도 가볍게 설명하도록 하겠습니다.

```
npm install --save google-map-react
```

npm install을 통해 쉽게 프로그램을 다운로드 가능합니다. 그럼 제가 구성한 컴포넌트를 하단에 먼저 보여드리고 설명하겠습니다.

```javascript
import GoogleMapReact from "google-map-react";

const Map = ({ center, zoom }) => {
  return (
    <div className="map">
      <GoogleMapReact
        bootstrapURLKeys={{ key: "##" }}
        defaultCenter={center}
        defaultZoom={zoom}
      ></GoogleMapReact>
    </div>
  );
};

Map.defaultProps = {
  center: {
    lat: 36.650879,
    lng: 127.468983,
  },
  zoom: 6,
};

export default Map;
```

제가 구성한 Map.js 컴포넌트입니다. 가장 먼저 맨 위에 우리가 다운로드 한 GoogleMapReact를 import 해주셔야 합니다. 이후 center와 zoom이라는 두 props 값을 가지는 map 변수를 구성합니다. 주목할 부분은 Google에서 제공하는 프로그램인 만큼 api에 대한 key값을 요구하는데요. `bootstrapURLKeys={{ key: '##'}}` 의 ##위치에 google에서 제공하는 key를 넣어주셔야 합니다. key값은 Googel cloud console에서 요청 가능합니다. 이후 저는 첫 시작 위치인 defaultCenter와 초기 줌 값 defaultZoom을 모두 props 값으로 지정해줬습니다.

이렇게 변수는 구성이 마무리됩니다. 뒤에 추가적으로 Map의 defaultProps값을 한국 위치로 적용해주었습니다(중심인 충청도 위치로 설정했습니다 ). 이 상태로 App.js에 import만 시켜주면 React에서 Google map 활용 준비가 마무리됩니다. 지도의 크기를 설정하기 위해서 Map의 className을 'map'으로 지정했습니다. 이 지정자를 통해 크기, 투명도, 위치 등을 CSS로 제어가 가능합니다.

이렇게 준비 과정은 마치구요. 다음 시간에 이 지도 api에 또 다른 정보를 제공하는 api를 통해 실질적으로 쓸모 있는 어플을 만들어 보도록하겠습니다. 감사합니다.
