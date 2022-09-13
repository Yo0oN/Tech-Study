---
created: 2022-08-24
modified: 2022-08-24
tag: [Java, NestedClass, Lambda]
title: Lambda
author: Yo0oN
category: [Java]
---

# Lambda

### 시작

자바는 병렬화를 위해 컬렉션을 강화하고, 그를 효율적으로 사용하기 위해 스트림을 강화했다.
또 스트림을 효율적으로 사용하기 위해 만들어진 함수형 프로그래밍이 람다이다.

람다 함수는 프로그래밍 언어에서 사용되는 개념으로, 익명함수(Anonymous Functions)를 지칭하는 용어이다.

---

## 1. Lambda?

자바 8에서 새로 추가된 기능으로, 함수를 식으로 표현한 것이다.

인터페이스가 가진 추상 메서드를 간단하게 구현하는데 도움을 준다.

```Java
interface Printable {
	void print(String s);
}

class Printer implements Printable {
	public void print(String s) {
		System.out.println(s);
	}
}

class Lambda {
	public static void main(String[] args) {
		Printable prn = new Printer();
		prn.print("Hello Lambda");
	}
}
```

^806ca6

람다가 나오기 전에는 인터페이스 Printable을 구현하는 Printer를 정의하여, print를 할 수 있었다.
하지만 print를 일회성으로 사용하기 위해 굳이 Printer를 정의하지 않고, 아래와 같이 간단하게 작성할 수 있다.

```Java
interface Printable {
	void print(String s);
}

class Lambda {
	public static void main(String[] args) {
		Printable prn = new Printer(){
			public void print(String s) {
				System.out.println(s);
			}
		}
		
		prn.print("Hello Lambda");
	}
}
```

익명클래스를 이용하여 Printer를 없애고, print를 할 수 있게 되었다.
위의 코드를 람다를 이용하게  다시 한번 단순하게 만들어보자.

```Java
interface Printable {
	void print(String s);
}

class Lambda {
	public static void main(String[] args) {
		Printable prn = (s) -> { System.out.println(s); };
		
		prn.print("Hello Lambda");
	}
}
```

^65b96f

람다를 이용하니 익명클래스를 이용할 때보다 더 간단해졌다.
(참고로 Printable 내부에 메소드가 하나만  존재하기 때문에 가능한 것이다.)


위의 Printable처럼 추상 메소드를 하나만 가진 인터페이스를 *함수형 인터페이스* 라고 하는데 람다식은 함수형 인터페이스에 유용하게 사용된다.



## 2. 사용법

람다식은 3부분으로 이루어진다.

```Java
매개변수 목록    화살표 토큰    처리식(리턴값)
(int x, int y)      ->      { return x + y; }
```

위에서 더 줄이는 것이 가능한데, 매개변수의 타입을 유추할 수 있는 경우 타입을 생략할 수 있다.

```Java
(x, y) -> { return x + y; }
```

또, 매개변수가 하나일 경우 소괄호도 지울 수 있고, 실행할 코드가 한 줄이라면 중괄호와 return 키워드도 생략 가능하다.

```Java
(x, y) -> x + y;
```



## 3. Variable Capture

내부에서 파라미터로 넘겨진 변수가 아닌 외부에서 정의된 변수를 참조하는 것을 Variable Capture라고 한다.

외부의 변수가 final이거나, effective final(사실상 final)일 경우 참조할 수 있다.
만약 상수가 아니라면 concurrency 문제로 컴파일 에러가 발생한다.


```Java
public class Test {
	public static void main(String[] args) {
		// 변경하는 곳이 없으니 effective final
		int baseNumber = 10;
		
		// 로컬 클래스 - 외부 변수 참조 가능
		class LocalClass {
			void printBaseNumber() {
				System.out.println(baseNumber); // 10
			}
		}

		// 익명클래스 - 외부 변수 참조 가능
		Consumer<Integer> intergerConsumer = new Consumer<Integer>() {
			@Override
			public void accept(Integer integer) {
				int baseNumber = 30;
				System.out.println(baseNumber); // 30
				System.out.println(this.baseNumber); // 10
			}
		}
		
		// 람다식일 경우 - 외부 변수 참조 가능
		IntConsumer printInt = (i) -> System.out.println(i + baseNumber);
	}
}


```




## 4. 메서드, 생성자 레퍼런스

메서드 레퍼런스는 람다를 이용하여 메서드를 참조한 것으로, 생성자는 그중에서 생성자를 참조한 것이다.<br>
메서드를 참조할 때는 `객체 레퍼런스::인스턴스메서드` 또는 `타입::static메서드` 처럼 사용하고, 생성자를 찹조할 때는 `타입::new` 처럼 사용한다.<br>
아래의 예시를 보자.

```java
public class Greeting{
	private String name;

	public Greeting() {
	}

	public Greeting(String name) {
		this.name = name;
	}

	public static String hi(String name) {
		return "hi " + name;
	}

	public String hello(String name) {
		return "hello " + name;
	}
}
```

예를들어 위와 같은 클래스가 있다.
그리고 해당 타입의 메서드와 생성자는 아래와 같이 참조한다.

```java
public class App {
	public static void main(String[] args) {
		// 생성자 참조
		Supplier<Greeting> greeting = Greeting::new;
		// 실제 생성자를 이용해 객체 생성
		Greeting greet = new Greeting.get();
		// 파라미터를 받는 생성자 참조
		Function<String, Greeting> stringGreet = Greeting::new();

		// static 메서드 참조
		// UnaryOperator : 특정 타입을 입력받아, 해당 타입을 리턴하는 함수형 인터페이스
		UnaryOperator<String> hi = Greeting::hi;
		// 실제로 실행
		hi.apply("Yoon"); // hi Yoon

		// 특정 객체의 인스턴스 메서드 참조
		UnaryOperator<String> hello = greet::hello;
		// 실제로 실행
		hello.apply("Yoon"); // hello Yoon

		// 임의 객체의 인스턴스 메서드 참조
		String[] names = {"Kee", "White", "to"};
		// Arrays.sort(T[] a, Comparator<? super T> c) 메서드는 배열을 하나 받은 후 
		// 뒤의 Comparator의 compare 메서드의 결과를 보고 정렬해준다.
		Arrays.sort(names, new Comparator<String>() {
			@Override
			public int compare(String o1, String o2){
				
			}
		})
		// 그런데 Comparator<String>을 구현하는 부분을 람다로 변경할 수 있다.
		// String의 compareToIgnoreCase는 문자열을 받아 현재 문자열과 다음 문자열을 비교해주는
		// 이미 정의되어 있는 Compareator.compare의 결과를 리턴한다.
		// 그래서 위의 식을 아래와 같이 나타낼 수 있다.
		Arrays.sort(names, String::compareToIgnoreCase);
	}
} 
```




## 5. 컬렉션 스트림에서 사용하기

```Java
Integer[] ages = {10, 20, 30, 25, 18, 58};

for (Integer t : ages) {
	if (i < 20) {
		System.out.println(i);
	}
}
```

배열 ages를 순회하기 위해서는 보통 위와 같이 사용할 것이다.
하지만 스트림 + 람다를 이용하면 아래와 같이 사용할 수 있다.

```Java
Arrays.stream(ages) // 스트림으로 변경
	.filter(age -> age < 20) // filter를 이용하여 ages 스트림 중 20 미만만 골라내기
	.forEach(age -> System.out.println(age)); // 반복문을 이용하여 스트림 차례로 출력
```



---

## 마무리

람다를 사용하는 것도 좋지만 코드를 읽을 때 읽기 쉽게 작성하라는 글을 본적이 있다.
람다식으로 간단하게 표현할 수 있는것이라면 사용하겠지만 읽기 복잡해진다면 앞으로도 사용은 잘 안하지 않을까 싶다..

그런데 또 자주 사용을 해야 읽기 쉬울것같기도하고.. 
역시 어렵군!


### 관련 문서
[[java.util.function - Functional Interface]]


### 참고
- 윤성우의 열혈 Java 프로그래밍
- [백기선님의 live-stydy](https://github.com/whiteship/live-study/issues) 15주차
