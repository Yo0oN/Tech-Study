---
created: 2022-07-31
modified: 2022-07-31
tag: [Java, NestedClass]
title: Nested Class
author: Yo0oN
category: [Java]
---

# Nested Class

### 시작
실제로 Nested Class를 이용할 일이 있을지는 모르겠지만, Lambda가 나오기 전에는 자주 사용했다고 한다.

내가 실제로 사용하지 않더라도 Lambda가 나온 이유와, 사용하기 위해서는 해당 내용에 대하여 알아두어야할것같다.

---

## 1. Nested Class?

클래스 안에 또 다른 클래스를 정의할 수 있는데, 클래스 내에 정의된 클래스를 Nested Class라고 한다.

```Java
class Outer {
	static class Nested {}
	class Inner{}
}
```

위와 같은 형태로 사용하고, 외부의 클래스는 Outer Class(외부 클래스), 내부의 클래스는 Nested Class라고 한다.

그리고 해당 클래스들은 다시 static 여부에 따라, 정의되는 위치에 따라 여러 종류로 나뉜다.



그리고 Nested Class들 중 Non-static 클래스는 Inner Class라고 한다.

또 Inner Class들의 정의되는 위치에 따라 다시 Member Inner Class, Local Inner Class, Anonymous Inner Class로 나뉘는데



## 2. Static Nested Class

Nested Class 들 중 static 선언이 가지는 특성이 반영된 클래스이다.
static이기 때문에 외부 클래스의 인스턴스와는 상관없이 Static Nested Class의 인스턴스 생성이 가능하다.

```Java
Class Outer {
	private static int num = 0;

	static class Nested1 {
		void add(int n) {
			num += n;
		}
	}

	static class Nested2 {
		int get() {
			return num;
		}
	}
}

class StaticNested {
	public static void main(String[] args) {
		Outer.Nested1 nested1 = new Outer.Nested1();
		nested1.add(5);

		Outer.Nested2 nested2 = new Outer.Nested2();
		System.out.println(nested2.get()); // 5
	}

}
```

Static Nested1, 2 클래스에서는 Outer 클래스의 내부에 있는 클래스이기 때문에 private임에도 `num`에 접근할 수 있다. (num이 static이 아니었다면 접근불가능하다.)

그리고 static의 특징을 가지고 있기때문에 인스턴스 생성 시에 Outer클래스가 생성되지 않았음에도  `Outer.Nested~` 와 같이 생성할수 있다.


## 3. Inner Class

Nested Class 들 중 static이 붙지 않은 클래스들을 말한다.
대신 정의되는 위치에 따라 다시 셋으로 나뉜다.

#### 3-1. Member (Inner) Class

인스턴스 변수, 인스턴스 메소드와 동일한 위치에 정의된다.

```Java
class Outer {
	private int num = 0;
	
	class Member {
		void add(int n) {
			num += n;
		}
		int get() {
			return num;
		}
	}
}

class MemberInner {
	public static void main(String[] args) {
		Outer outer1 = new Outer();
		Outer outer2 = new Outer();
		
		Outer.Member outer1member1 = outer1.new Member();
		Outer.Member outer1member2 = outer1.new Member();
		
		Outer.Member outer2member1 = outer2.new Member();
		Outer.Member outer2member2 = outer2.new Member();
		
		outer1member1.add(5);
		System.out.println(outer1member2.get()); // 5
		
		outer2member1.add(10);
		System.out.println(outer2member2.get()); // 10
	}

}
```

Static Nested와는 다르게 Outer클래스가 먼저 생성된 후 Member 클래스를 생성할 수 있다. > 멤버 클래스의 인스턴스틑 외부 클래스에 종속적이다.

Member Inner 클래스에서는 Outer 클래스의 내부에 있는 클래스이기 때문에  `num`에 접근할 수 있다.

그리고  outer1member1과 outer1member2는 같은 객체인 outer1에서 만들어졌기 때문에 `num`을 공유하고 있다.

Member Inner Class의 경우 클래스의 정의를 감추어야할 때 사용한다.

```Java
interface Printable {
	void print();
}

class Papers {
	private String con;
	public Papers(String s) { con = s; }
	public Printable getPrinter() {
		return new Printer(); // 멤버 클래스 반환
	}
	
	private class Printer implements Printable {
		public void print() {
			System.out.println(con);
		}
	}
}

class UseMemberInner {
	public static void main(String[] args) {
		Paper p = new Papers("안녕!");
		Printable prn = p.getPrinter();
		prn.print(); // 안녕!
	}
}
```

위와같이 멤버 클래스가 private로 선언되어 외부클래스인 Papers에서만 생성이 가능하게되고, 외부에서는 `getPrinter()`가 어떤 것을 반환하는지 정확히 알지 못한채로 사용하고 있다.

이런 상황을 클래스의 정의가 감추어진 상황이라 한다.
이렇게 감추게된다면 `getPrinter()`에서 `Printer`대신 다른 인스턴스를 반환하도록 변경하더라도 `getPrinter()`를 사용하는 외부에서는 그에 맞춰 수정해주지 않아도 된다는 장점이 있다.

대표적인 예로는 컬렉션 프레임워크에서 반복자 Iterator를 사용할 때 `iterator()`가 있다.
해당 메서드가 무엇을 반환하는지 모르지만 Iterator 인터페이스를 구현한 무언가를 반환한다 정도만 알아도 사용하는데 문제는 없다.


#### 3-2. Local (Inner) Class

중괄호 내, 특히 메소드 내에 정의한다. (반복문이나 조건문 내부에서 사용할수도 있다.)

```Java
class Outer {
	void method() {
		class LocalInner {}
	}
}
```

Member Inner Class와 비슷하지만 대신 위치가 다를 뿐이다.

```Java
interface Printable {
	void print();
}

class Papers {
	private String con;
	public Papers(String s) { con = s; }
	public Printable getPrinter() {
		class Printer implements Printable { // 로컬 클래스
			public void print() {
				System.out.println(con);
			}
		}
		return new Printer(); // 로컬 클래스 반환
	}
}

class UseMemberInner {
	public static void main(String[] args) {
		Paper p = new Papers("안녕!");
		Printable prn = p.getPrinter();
		prn.print(); // 안녕!
	}
}
```

대신 위와의 차이점은 괄호 내에서 정의되기 때문에 `private` 선언을 하지 않더라도 외부에서 접근이 불가능하고, 더 깊이 감출수 있다는 차이가 있다.


#### 3-3. Anonymous (Inner) Class

이름이 존재하지 않는 클래스로, Lambda와 연관이 있다.
위의 Local Class에서 메서드 안에 클래스를 넣었는데 이를 좀 더 간단히 하면 아래와 같다.

```Java
interface Printable {
	void print();
}

class Papers {
	private String con;
	public Papers(String s) { con = s; }
	public Printable getPrinter() {
		return new Printable() { // 익명 클래스 정의, 인스턴스 생성을 동시에!
			public void print() {
				System.out.println(con); 
			}
		}
	}
}

class UseMemberInner {
	public static void main(String[] args) {
		Paper p = new Papers("안녕!");
		Printable prn = p.getPrinter();
		prn.print(); // 안녕!
	}
}
```

참고로 위와 같은 코드는 자바에 람다가 등장하기 전에 자주 사용하던 스타일이다.


---


## 마무리

사실..아직도 내가 Nested Class를 만들 일이 실제로 있을지는 모르겠다.

### 관련 문서
[[Lambda]]


### 참고
- 윤성우의 열혈 Java 프로그래밍

