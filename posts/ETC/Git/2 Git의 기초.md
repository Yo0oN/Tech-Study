---
created: 2022-10-16
modified: 2022-10-16
tag: [Git]
title: Git의 기초
author: Yo0oN
category: [Git]
---

# Git의 기초

---

## 1. Git 저장소 만들기

저장소를 만드는데는 두 가지 방법이 있다.
첫 번째는 로컬 디렉토리를 선택해서 Git 저장소를 적용하는 방법
두 번째는 다른 Git 저장소를 `clone` 해오는 방법

#### 기존 디렉토리를 Git 저장소로 만들기

```Git
git init
```

위 명령어를 실행하면 `.git`이라는 디렉토리가 생긴다.
해당 디렉토리 내부에는 Git 사용에 필요한 뼈대 파일이 들어있다.

![git init](https://user-images.githubusercontent.com/53729311/196037383-aa285440-861b-43f5-bfec-730bbf343223.png)


#### 다른 Git 저장소를 clone해오기

```Git
git clone {저장소 url}
```




## 2. 파일의 현재 상태

```Git
git status
```

위의 명령어는 파일의 상태를 알 수 있도록 해준다.

파일의 상태에는 4가지 상태가 있다.

![git-scm.com](https://user-images.githubusercontent.com/53729311/196038935-06085efc-59a3-422b-881a-5cd0e365dc75.png)

1. Untracked
	- Git이 추적하지 않는 파일
	- 추적하지 않는 파일이 수정된다면 `git status` 명령을 실행했을 때 파일 앞에 `??`가 표시된다.
2. Unmodified
	- Git이 추적 가능한 파일
	- 아직 수정되지 않은 상태이다.
3. Modified
	- Git이 추적 가능한 파일
	- 수정이 된 파일이다.
4. Staged
	- Git이 추적 가능한 파일
	- 커밋 직전의 파일이다. = 커밋이 가능한 상태의 파일



#### 파일 추적하기

```Git
git add {file name}
git add {directory}
```

새로 파일을 만들게되면 추가하지 않는 이상 Git이 추적하지 못하는 파일로 만들어진다.
해당 파일을 Git이 추적하게 하려면 `git add`를 이용하면 된다.

![git status](https://user-images.githubusercontent.com/53729311/196039472-5d1ecc57-df1d-4254-92fd-c82aa295dc50.png)

두개의 파일을 만들고 `git add name` 명령어를 입력해본 후  `git status`로 상태를 확인하니 위와 같이 보인다.
```Plain Text
menu : Untracked 상태의 파일
name : Tracked 상태의 파일, Commit이 가능한 Staged 상태의 파일
```

참고로 Staged 상태의 파일을 커밋하지 않은 채로 다시 수정할 경우 추가된 내용은 추적중이지만 Staged 상태가 아니다.
추가로 수정된 내용도 커밋하고 싶다면 `git add`를 통해 Staged 상태로 만들어주자.

![git status2](https://user-images.githubusercontent.com/53729311/196040171-2bcda6b6-8360-4f26-9424-3d6d727c21ba.png)



#### 수정 내용 확인하기

Git이 추적중인 파일이라면 어떤 내용이 변경되었는지 확인할 수도 있다.
```Git
git diff
```

![git diff](https://user-images.githubusercontent.com/53729311/196040510-35072b86-eb61-43c6-bed0-9067e8f227b9.png)

아래의 `+코난`은 추적 중인 name 파일이 처음 `git add`로 Staged 상태가 된 이후에 추가된 내용이다.



#### 변경사항 커밋하기

```Git
git commit
```

위에서 추적 중이고, Staged 상태의 파일은 Commit을 할 수 있다.

![git commmit](https://user-images.githubusercontent.com/53729311/196040958-9bfb1551-a1e6-4f64-bd11-ec6fc1f94d2e.png)

`git commit` 명령어를 입력하면 앞에 커밋 메세지를 입력하라는 말과 커밋 될 파일, 추적되지 않는 파일을 보여준다.
커밋 제목과 내용을 적은 뒤 저장하면 수정된 파일의 수와 몇 줄이 추가되었는지 등의 내용이 보여지고, `git log` 명령어를 이용하면 커밋 된 것을 확인할 수 있다.

![git log](https://user-images.githubusercontent.com/53729311/196041170-bdedf39a-7301-45db-9aa3-892627202043.png)




## 3. 되돌리기

#### 마지막 커밋 수정하기

```Git
git commit --amend
```

amend라는 단어에는 개정하다, 고치다, 수정하다 라는 뜻이 있다.
커밋 후 아무것도 수정하지 않고 위 명령어를 사용하면 커밋 메시지만 수정할 수 있다.

새로운 커밋을 만드는 것이 아닌 덮어쓰기되는데, 날짜나 시간은 변하지 않는다.


#### Unstaged 상태의 파일을 파일을 수정 전 상태로 되돌리기
```Git
git restore {file name}
```

참고로 해당 명령어는 `git status`를 하면 unstaged 쪽에서도 확인할 수 있다.

![git status3](https://user-images.githubusercontent.com/53729311/196041501-374146f2-d694-4c36-ad61-b1fe4a8bf523.png)


#### Staged 파일을 Unstaged 상태로 변경하기

```Git
git restore --staged {file name}
```

이전 버전에는 reset이지만, 2.23 부터 restore로 변경되었다.
이 명령어도 `git status`를 하면 확인할 수 있다.

![git resotre](https://user-images.githubusercontent.com/53729311/196044368-b0c22045-10aa-4571-b747-ae4cf7805c69.png)




## 4. 기타 기능들

#### 파일 삭제하기

```Git
git rm {file name} == rm {file name}; git add {file name}
```

추적 중인 파일을 삭제한 후 상태를 확인하면 `Changed not staged for commit`이라는 문구를 볼 수 있다.
삭제된 내용이 Staged되지 않은 것이다.

![git status3](https://user-images.githubusercontent.com/53729311/196041501-374146f2-d694-4c36-ad61-b1fe4a8bf523.png)

여기서 `git add` 명령어를 이용하면 삭제된 내용을 Staged 할 수 있지만, 파일 삭제와 해당 내용을 Staged 상태로 만드는 일을 한번에 하고 싶댜면 `git rm` 명령어를 이용하자.

![git status4](https://user-images.githubusercontent.com/53729311/196041539-b3f2ba79-49f8-47ab-8649-fb9d1b12d1ad.png)



#### 파일 이름 변경하기

```Git
git mv {file name} {new file name}
== mv {file name} {new file name}; git rm {file name}; git add {new file name}
```

Git은 파일 이름이나 이동을 명시적으로 관리하지는 않는다.
만약 Staged 상태의 파일 이름을 변경하게 된다면 아래와 같이 기존 파일은 삭제하고 새로운 파일을 생성한것처럼 보인다.

![change name](https://user-images.githubusercontent.com/53729311/196042501-e1a99541-e3ea-4c16-8171-e87b474b6434.png)

물론 여기서 `git rm`과 `git add`를 더 진행할 수도 있지만, 이 모든 작업을 한번에 하고 이름이 변경된 파일까지 Staged 상태로 만들고 싶다면 `git mv` 명령어를 이용하자.



---


### 참고
- [Git](https://git-scm.com/book/ko/v2)
