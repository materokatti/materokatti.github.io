---
layout: single
title: "TypeScript 모듈"
description: "Typescript module"
tags: [TS]
comments: true
published: true
categories: TS
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---

 이번엔 타입스크립트의 모듈에 대해 알아보려고 합니다.

```typescript
// math.ts
export interface Triangle {
  width: number;
  height: number;
}

// index.ts
import { Triangle } from './math.ts';

class SomeTriangle implements Triangle {
  // ...
}
```

위는 공식문서의 예시인데요. 이렇게 export와 import를 할 수 있다는 것이 유용합니다.

```typescript
import { WheatBeerClass } from './index.ts';

class Cloud extends WheatBeerClass {
  
}
```

ES6의 import와 동일하게 사용 가능합니다.



## 명령어에 따른 컴파일 방식 

```
# commonjs 모드인 경우
tsc --module commonjs Test.ts

# amd 모드인 경우
tsc --module amd Test.ts
```

타입스크립트는 컴파일 과정에서 모드를 정해줄수 있습니다. 모드 결정에 따라 서로 다른 형태로 컴파일 되는 거죠. 형식을 확인하고 필요한 요소로 컴파일 하면 됩니다.

```typescript
// SimpleModule.ts
import m = require("mod");
export let t = m.something + 1

// AMD / RequireJS SimpleModule.js 
define(["require", "exports", "./mod"], function (require, exports, mod_1) {
  exports.t = mod_1.something + 1;
});

// UMD SimpleModule.js
(function (factory) {
  if (typeof module === "object" && typeof module.exports === "object") {
    var v = factory(require, exports); if (v !== undefined) module.exports = v;
  }
  else if (typeof define === "function" && define.amd) {
    define(["require", "exports", "./mod"], factory);
  }
})(function (require, exports) {
  var mod_1 = require("./mod");
  exports.t = mod_1.something + 1;
});
```

