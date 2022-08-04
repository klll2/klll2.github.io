---
layout: post
title: "ex [React] .gitignore에 추가했는데 왜 자꾸 추적을 할까? 추적 삭제하는법!"
subtitle: "[React] .gitignore에 추가했는데 왜 자꾸 추적을 할까? 추적 삭제하는법!"
category: devlog
tags: tips react
image:
  path: /assets/img/reactlogo.png
---

vscode 에서 환경 변수를 만들어 작업을 하고 `.gitignore` 에 추가를 했다.  
그런데? 왜 자꾸 깃헙에 올라가지?? 아니 왜이러는거야 분명히 추가되었는데!!  
(DS_Store도 같은 문제때문에 골머리를 앓은 적이 있다.)

코드에 대한 PR을 받고나서 한번 추적한 것은 캐쉬에 저장이되어 `.gitignore` 추가해도  
계속 추적을 하는 것을 알게되었다.

### 이미 추적 중인 캐쉬 삭제하기

깃에서 이미 추적하고 있는 것을 삭제하자

```
git rm --cached <file이름>
```

이렇게 하면 해당 파일을 더이상 추적하지 않고 다음 push 때 깃헙에서 파일을 삭제한다.
전부 다 해주는 것도 있지만 개인적으로는 문제 생길까봐 필요 한 것만 삭제한다.

### 모든 캐쉬를 삭제하고 스테이징 Area에 올리기

```
git rm -r --cached . git add .
```
