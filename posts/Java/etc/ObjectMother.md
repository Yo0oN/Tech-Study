---
created: 2022-10-26
modified: 2022-10-26
tag: [Java, Test]
title: ObjectMother
author: Yo0oN
category: [Java]
---

# Object Mother

인강을 보던 중 알게된 단어로 처음 들어보는 단어라 찾아보게되었다.

fixture : 고정되어 있는 물체
→ 테스트를 하는데 있어서 필요한 부분 또는 조건을 미리 준비해놓은 고정된 리소스 혹은 코드들

mock : 모조품
→ 실제 객체의 행동을 흉내내는 객체

---

## 1. Object Mother?

테스트 시 예제 객체를 만드는데 도움을 주는 클래스
factory pattern에서 시작되었다.

테스트를 작성할 때는 많은 예시 데이터가 필요하다.

예를들어 직원의 병가를 계산하는 테스트를 하려면 직원이 필요하다. 하지만 직원 객체를 만들기 위해서는 직원의 결혼 상태, 피부양자 수, 급여 이력 등 여러 데이터가 필요하고, 그와 관련된 객체도 생성해야한다. 그렇게 객체를 만들다 보면 직원 객체가 만들어진다. 그리고 이렇게 여러 고정된 데이터가 하나의 세트로 묶여있는 묶음을 test fixture라고 한다.

이런 fixture를 여러개 만들다 보면 fixture들만 만들어주는 공장(factory object)을 필요로 할것이다.

그리고 이 공장들을 Object Mother라고 부른다.


### 장점

-   테스트에서 중복되는 코드를 줄일 수 있다. → 쉬운 유지보수
-   테스트 작성이 쉬워진다. → 테스트 코드 작성에 부담이 줄어든다.
-   생성하려는 테스트 데이터가 복잡할수록 Object Mother를 만들면 편하다.

### 단점

-   많은 테스트들이 Mother의 데이터에 의존한다. (결합도가 높아진다)
    -   클래스를 변경하면 테스트들도 변경을 해야할 수 있다.
-   Object Mother가 너무 많은 책임을 져서 God Class가 될수도 있다.
    -   God Class / God Class
        -   하나의 책임을 가지지 않고, 여러 개의 책임을 가지게 되는 클래스로, 객체지향 프로그래밍에서 단일 책임 원칙(S)을 무시한 클래스이다.


참고!
Java에서 Object Mother를 만들 때 도움을 주는 [easy-random](https://github.com/j-easy/easy-random) 라이브러리가 있다.
필요한 데이터들을 랜덤으로 만들어준다.

---


### 관련 문서
[ObjectMother]([https://martinfowler.com/bliki/ObjectMother.html](https://martinfowler.com/bliki/ObjectMother.html))