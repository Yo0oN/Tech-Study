---
created: 2022-09-13
modified: 2022-09-13
tag: [Java, util, Functional Interface]
title: java.util.function - Functional Interface
author: Yo0oN
category: [Java]
---

# functional interface

---

## 1. function package

java8에서 추가된 기능으로, 추상메서드가 하나만 있는 인터페이스들이 모여있다.


## 2. functional interface

추상 메소드가 하나만 존재하는 인터페이스를 functional interface 함수형 인터페이스 라고 한다.

@FunctionalInterface 어노테이션을 이용하여 해당 인터페이스가 함수형 인터페이스임을 명시적으로 나타낼 수 있다. (없어도 된다.)


객체지향 언어인 java를 사용하다보면 함수형 언어와 비교했을 때 상대적으로 코드가 길어보인다.

![[Lambda#^806ca6]] 

print를 하려고 했을 뿐인데..

이때 함수형 인터페이스와 람다식을 이용하면 인터페이스를 인스턴스화 할 때 익명 클래스를 길게 구현하지 않고 짧고 간단하게 구현할 수 있다.

![[Lambda#^65b96f]]


위처럼 함수형 인터페이스와 람다식을 이용하면 인터페이스를 간단히 구현할 수 있는데, function 패키지에는 자주 사용할것같은 함수형 인터페이스들을 미리 모아두었다.

---


### 관련 문서
[[Lambda]]

