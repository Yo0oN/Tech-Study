---
created: 2022-10-17
modified: 2022-10-17
tag: [Git]
title: tag
author: Yo0oN
category: [Git]
---

## 1. tag

깃은 각 시점을 해시값으로 관리하고있는데, 태그는 사람이 알기 쉽게 문자로 적어둔 것을 말한다.
그리고 태그를 통해 이전 작업 시점으로 돌아갈 수 있다.


### 태그 붙이기

#### Lightweight tag

아무 정보를 저장하지 않고 만들어진 태그이다.
임시로 만들 경우에 사용하면 좋다.

```Git
git tag {name}
```

태그를 만들 때 추가 옵션을 사용하지 않고 이름만 달아주면 된다.

#### Annotated tag

태그를 만든 사람의 이름, 만든 날짜, 메시지 등이 함께 저장되는 태그이다.

```Git
git tag -a {name} -m {메시지}
git tag -a {name} {이전 커밋 체크섬}
```


### 태그 조회하기

```Git
git tag
```


### 태그 checkout 하기

```Git
git checkout {tag name}
```



### + branch vs tag

둘 모두 특정 시점에 대한 해시값을 가지고 레파지토리를 관리하는데 사용한다.
대신 브랜치는 작업이 진행될 때마다 가지는 해시값이 계속 변경되지만, 태그는 고정된 해시값을 계속 가지고 있다.

+`.git/refs/tags` 경로로 가면 해당 repo에 있는 태그를 확인할 수 있다.




---


### 참고
- [Git](https://git-scm.com/book/ko/v2)
