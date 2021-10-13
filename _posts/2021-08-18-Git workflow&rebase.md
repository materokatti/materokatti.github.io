---
layout: single
title: "Git workflow & rebase"
description: "Git workflow & rebase"
tags: [GIT]
comments: true
published: true
categories: GIT
typora-root-url: ../assets/images
sitemap:
  changefreq: daily
  priority: 1.0

---



#### Git workflow

 브랜치를 만드는 이유는 main 브랜치와 작업 공간을 분리해 문제가 생길 상황을 방지하기 위함이다. 이를 위해 깃 업무는 다양한 브랜치를 만들어 이런 문제를 체크, 테스트, 방지한다. 먼저 어떤 종류의 브랜치가 있는지 알아보자.

- main
- develop: 메인에서 develop을 따 줍니다. 개발 단계에서 완료된 코드가 여기 있죠.
- feature: develop에서 분리 해준 코드입니다. 기능 개발 할때 사용합니다.
- release: develop이 완료되면 release branch를 만들어 배포 준비를 합니다. 문제가 있으면 고치기 위해 다시 develop으로 가거나, 문제가 없다면 main으로 합쳐줍니다.
- hotfix: main의 마이너 업데이트로 급한 문제가 생겼을 때 main에서 바로 따서 main에 붙여준다. 급한 불을 끄면 다시 develop과 feature를 통해 문제를 다시 해결한다.

 이렇게 브랜치를 나누는 이유는 앞서 말했듯, 배포 단계에서 자료를 안전하게 관리될 수 있도록 하기 위함이죠.



#### Merge와 Rebase 

 일반적인 머지의 경우 커밋이 겹쳐지고 머지를 진행하면 필수적으로 merge 커밋이 생긴다. 이렇게 되면 작업이 진행될 수록 불필요한 커밋이 많아지고 history가 복잡해진다. Base 커밋은 feature가 잘려나온 첫 커밋이다. rebase는 이 베이스를 전환해 주는 것이다. rebase를 통해 이 베이스 지점을 최신 머지의 마지막 지점으로 바꿔주는 것이다. 이렇게 되면 커밋이 겹치지 않고 분리되어 로그를 살피는 것이 훨씬 편해진다. 

 그러나 rebase에도 커밋이 많아질 경우 conflict가 발생하는 문제가 있다. 이 때문에 커밋이 3번 이상 진행되면 rebase를 해주는 것이 좋다. 거기에 squesh처럼 커밋을 깔끔하게 정리해서 히스토리 추적을 도와주는 명령어도 있다.



#### Rebase 명령어

```
git rebase -i main
```

가장 많이 사용될 rebase 명령어로 커밋을 줄이거나 master branch 내용을 merge 할 때 사용된다.

```
git add .
git rebase --continue
```

 충돌이 생길 경우 해결하는 프로세스이다. 컨플릭트는 커밋을 기준으로 생기기 때문에 커밋을 진행하면 또 다른 충돌요소가 생긴다. 그래서 add 만 하고 rebase를 진행해준다. rebase는 모든 커밋에 대한 충돌이 마무리 될 때 까지 진행해준다. 그 때문에 문제 해결 중에는 --continue를 써 줘야 한다. 

```
git push origin feature/main -f 
```

처음으로 rebase 후 push 하면 에러가 생긴다. -f 로 강제로 업로드하면 해결되니 강제 push를 진행해도 괜찮다. 