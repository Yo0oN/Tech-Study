|작성일|수정일|
|:----|:----|
|2020-11-13|2020-11-13|

## 1. java.lang.String

String은 문자열 관련 클래스이다.<br>
String 클래스를 살펴보면 아래와 같이 시작된다.<br>
```java
public final class String extends Object
  implements Serializable, Comparable<String>, CharSequence
```
final 클래스이기 때문에 해당 클래스를 상속받은 클래스는 더이상 없고, Serializable는 객체를 파일로 저장하거나, 다른 서버에 전송 하도록 해주는 인터페이스이다.<br>
Comparable은 두개의 문자열을 비교하여 결과를 int로 알려주는 메서드인 compareTo()를 가진 인터페이스이며,
CharSequence는 문자열을 다루기 위한 클래스라는 것을 명시적으로 나타내는 인터페이스이다.(문자열을 다루는 StringBuilder와 StringBuffer에도 사용된다.)

## 2. 메서드들

|메서드|설명|
|----|----|
|getBytes()|기본 캐릭터 셋의 바이트 배열 생성|
|getBytes(Charset charset)|지정 캐릭터 셋 객체 타입의 바이트 배열 생성|
|getBytes(String charsetName)|지정 캐릭터 셋 객체 타입의 바이트 배열 생성|
|copyValueOf(char[] data)|char 배열의 내용을 문자열로 반환한다.|
|copyValueOf(char[] data, int offset, int count)|char 배열의 offset부터 count개를 문자열로 반환한다.|
...

이 외에도 여러 메서드들이 있다. 필요한 것들을 찾아보려면  메서드들을 더 보고싶다면 [String](https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/lang/String.html)을 살펴보자.
> 개인 정리노트는 [notion](https://www.notion.so/yoonstechstudy/String-Class-52673cdd1a0f453bac3d227e7f66ae46)으로..

#### 사용시 주의 할 메서드

- equals(Object object)
  String은 참조객체이기 때문에 ==를 사용하여 String의 내용을 비교하면 두 String 객체가 같은 참조주소를 가지고 있지 않을수도있으니 다르다고 나올 가능성이 있다.<br>
  String 클래스의 equals 메서드를 살펴보면 내부에서 두 String 객체의 참조주소가 아닌 주소가 참조하고 있는 값을 가져와서 비교하도록 overriding 되어있다.<br>
  만약 Strnig 끼리 값을 비교해야 하는 일이 있다면 equals를 사용하자. 대소문자 구분 없이 비교하고싶다면 equalsIgnoreCase(Object object) 메서드를 사용하자.

- compareTo(String anotherString)
  compareTo 메서드도 문자열의 값이 같은지 확인해주는 메서드이다.<br>
  내부를 보면 일단 두 분자열의 길이가 차이나는지 확인하고, 두 문자열을 각자 char 타입 배열에 넣어 ASCII 코드값을 한글자씩 비교한다.<br>
  만약 결과로 0이 나왔다면 두 문자열이 같은것이고, 양수가 나온다면 기본값의 길이가 더 길거나, 문자열이 달라지기 시작하는 부분의 기본 문자열의 ASCII 코드값이 더 큰 것이다.
  음수가 나온다면 반대로 비교 중인 anotherString의 길이가 더 길거나, ASCII 코드값이 더 큰 것이다.<br>
  두 문자열의 거리를 나타내기 때문에 정렬시 이용하면 좋다.

- intern()
  다른 언어로 작성된 것을 Java에서도 사용 가능하도록 만들어둔 native 메서드이다.<br>
  문자열은 값이 저장될 때 Constant Pool에 저장되어 GC에 의해 삭제되기 전까지 재사용이 가능하다.<br>
  ```java
  String a = "Hi";
  String b = "Hi";
  ```
  그래서 이렇게 하나의 클래스 안에서 두 객체를 생성하면 풀에는 두개의 Hi가 아닌 하나의 Hi만 생성되고, a와 b는 같은 Hi를 참조하고 있다.
  그렇지만, 생성자를 통해 문자열을 생성하면 재사용이 아닌 새로운 객체를 생성하게 되어 풀에 Hi가 있더라도 새로운 Hi를 만들어 참조한다.<br>
  값을 재사용 하지 않고 해당 값을 가진 객체가 여러개가 된다면, GC가 삭제하기 전까지 같은 객체 여러개가 풀에 있으므로 메모리를 계속 사용할것이다.<br>
  이때 intern()을 생성자와 함께 사용하면 풀에 중복된 것이 있다면 새로 만들지 않고 재사용을 하게 해준다.<br>
  얼핏들으면 좋아보이지만, 해당 메서드를 사용하면 생성자를 통해 객체를 만들고, 풀을 찾아보며 사용하려는 값이 있는지 찾는 시간이 추가로 들기 때문에 사용하지 않을 때보다 시간이 더 걸린다.<br>
  특별한 일이 없다면 사용할일이 없는 메서드이다.
  > 추가로 Java6까지 String Constant Pool은 Heap이 아닌 Perm 영역에 위치하여 intern()을 사용한 값은 GC의 대상이 될 수 없었다고 한다.<br>
  > 그래서 해당 객체를 더이상 사용하지 않는 때가 오더라도 삭제되지 않고 메모리에 남아있어 오히려 메모리를 더 낭비하는 현상이 있었으나,
  Java7부터는 constant pool이 Heap 영역으로 이동하여 intern을 사용하더라도 GC의 대상이 될 수 있게되었다.<br>
  > 그게 아니더라도 사용할일이 많아보이진 않는 메서드다..


## 3. 문자열의 단점

문자열은 immutable 객체, 즉 변하지 않는 객체이다.<br>
문자열을 사용하다 보면 + 연산을 이용하여 문자열을 이어붙일 수 있다.
```java
String a = "Hello";
a = a + " World!";
```
위의 a는 "Hello"일때나, 연산자를 이용하여 "Hello World!"로 수정하였을 때나 겉보기에는 같은 객체처럼 보인다.<br>
하지만 실제로 내부에서는 기존 a = "Hello"를 버리고 새로운 객체인 "Hello World!"를 새로 생성하도록 작동하고 있기 때문에 + 연산자를 자주 쓰면 GC가 삭제하기 전까지 메모리를 낭비하게 된다.<br>
그러니 문자열이 변경되지 않을 경우에만 String을 사용하고, 문자열이 자주 변경될 것 같다면 새로운 객체를 만들지 않고, 기존 객체의 크기를 늘려 뒤에 붙여주는 StringBuilder()나 StringBuffer()를 사용하도록 하자.<br>

추가적으로 JDK 5 부터는 String의 + 연산을 사용하더라도 컴파일 시 알아서 StringBuilder로 변환시켜주고 있다.<br>
하지만 concat() 메서드나, 반복문을 이용할 경우는 여전히 StringBuilder로 변환하지 않고 여전히 새 객체를 생성하고 있으니 String의 + 연산을 사용할 때는 주의하자.
