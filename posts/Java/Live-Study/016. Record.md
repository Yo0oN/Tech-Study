---
created: 2022-10-28
modified: 2022-10-28
tag: [Java]
title: Record
author: Yo0oN
category: [Java]
---

## 1. Record


JDK 14에서 처음 소개된 후 JDK 16에서 정식으로 사용 가능하게 되었다.

상수만 모아두는 enum과 비슷하게 class의 한 종류이다

변경되지 않는 데이터(불변 - final)를 담고있으며 생성자, 접근자(getter)같은 필수적인 메소드가가 기본으로 포함되어있으며, 순수하게 데이터를 담는데 사용된다. `plain data carriers`


### record 이전...

```java
final class Rectangle implements Shape {
		// 모든 멤버변수는 final로 선언
    final double length;
    final double width;
    
		// 생성자와 접근자 외 다른 메소드 없음
		// 생성자
    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }
    
		// 접근자 getter
    double length() { return length; }
    double width() { return width; }
}
```

record 이전에는 모든 필드에 final을 사용한 후, 생성자를 통해 값을 할당하고, 해당 필드에 접근하려면 getter를 이용해야했다.



### record 이후...

```java
record Rectangle(float length, float width) { }
```

-   final 클래스로 생성되고, 상속이 불가능하다.
-   absctract 추상 클래스로 생성할 수 없다.
-   인터페이스 구현은 가능하다, 다른 클래스를 상속받을수는 없다.
-   모든 필드는 `private final`로 생성된다.
-   생성자와 접근자를 만들지 않아도 자동으로 생성한다.
-   두 record 객체가 동일한 타입이고, 구성요소가 동일한 경우 두 객체를 같다고 인식한다.
    -   `equals()`, `hashCode()` 오버라이딩을 자동으로 해줌
-   toString()의 경우 이름과 함께 모든 레코드 구성 요소의 문자열을 포함하도록 오버라이딩된다.
    ![image](https://user-images.githubusercontent.com/53729311/198673827-274854df-c1dd-476d-a092-c00e4585f1af.png)

-   모든 record는 `java.lang.Record`를 상속받는다.
-   각 필드에 어노테이션을 달 수 있다.
    ```go
    record Rectangle(
        @GreaterThanZero double length,
        @GreaterThanZero double width
    ) { }
    ```
    


## 2. Compact Construtors

-   record에도 기본 생성자 외에 다른 생성자를 추가할 수 있다.
    
    하지만 record의 생성자는 매개변수를 가지지 않는다.
    
    그리고 이 생성자를 _compact constructor_라고 부른다.
    

```go
record HelloWorld(String message) {
	public HelloWorld {
		java.util.Objects.re
	}
}
```


## 3. 추가로 읽어보면 좋은 글

-   Record를 entity로 사용하기? 불가능!
    -   JPA를 사용하려면 프록시 생성을 위해 entity가 불변이면 안된다. 그래서 불변객체인 record를 사용하게된다면 `User declared non-static fields id are not permitted in a record` 에러가 뜬다.
    -   쿼리 결과를 매핑할 때 객체를 인스턴스화 할 수 있도록 매개변수가 없는 생성자가 필요하다. 하지만 record는 매개변수가 없는 생성자를 지원하지 않는다.
    -   접근자 메소드가 getXX() 형태가 아닌 필드명을 그대로 사용하고있기 때문에 쿼리 결과 처리 후 수행되는 getter, setter를 사용할 수 없다.
-   대신 DTO를 record 타입으로 사용하기에는 적당할듯하다.

[[Java]자바 record를 entity로?](https://velog.io/@power0080/java%EC%9E%90%EB%B0%94-record%EB%A5%BC-entity%EB%A1%9C)

---


### 관련 문서
[[Java]자바 record를 entity로?](https://velog.io/@power0080/java%EC%9E%90%EB%B0%94-record%EB%A5%BC-entity%EB%A1%9C)
[Java docs](https://docs.oracle.com/en/java/javase/16/language/records.html)