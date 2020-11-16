|작성일|수정일|
|:----|:----|
|2020-11-13|2020-11-13|

--------

### 목표

자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.

### 학습할 것
- JVM이란 무엇인가
- 컴파일 하는 방법
- 실행하는 방법
- 바이트코드란 무엇인가
- JIT 컴파일러란 무엇이며 어떻게 동작하는지
- JVM 구성 요소
- JDK와 JRE의 차이

## 1. JVM이란 무엇인가?

### JVM - Java Virtual Machine

JVM은 자바 프로그램을 실행시키도록 해주는 가상머신으로 크게 두가지 기능이 있다.

### Write once, run anywhere

Java 언어를 설명하기 위한 슬로건으로, Java로 작성된 프로그램은 한번 작성하면 어느 장치, 운영체제에서나 실행 가능하도록 해주는 언어라는 것을 뜻한다.~~*(Write Once, Debug Everywhere)*~~

처음 자바를 사용하기 전 컴퓨터 프로그램들은 같은 프로그램이어도 여러 운영체제에 맞춰 다르게 작성해야 했다.
그런데 1995년 등장한 Java는, 프로그램을 한 번만 작성하면 Java 프로그램과 운영체제 사이에서 JVM이 동작하여 운영체제, CPU등에 관계없이 동일하게 Java 프로그램이 동작하도록 해주었다.<br>
그래서 Java언어의 특징 중 운영체제에 독립적이다라는 점은 JVM 덕분에 나온 이야기이다.

### Garbage Collector

어떤 언어들은 프로그래머가 해당 프로그램의 메모리 관리를 모두 해야한다.<br>
하지만 JVM은 Java 프로그램에서 사용하지 않는 메모리를 식별하고, 사용하지 않는다면 제거해주는 Garbage Collection 프로스세스를 통해 메모리 관리를 대신 해준다.

<br>

## 2. 컴파일 하는 방법 & 실행하는 방법

### 2-1. Compile?

프로그래밍 용어에서 *Compile(컴파일)* 은 특정 프로그래밍 언어로 작성된 문서를 0과 1만 이해하는 컴퓨터가 이해할 수 있도록 기계어로 바꿔주는 과정이다.<br>
그리고, 컴파일을 해주는 기계를 *Compiler(컴파일러)* 라고 부른다.<br>
여기서 컴파일 하기 전 사람이 작성한 코드를 '원시코드' 또는 '소스코드' 라고 부르며, 결과로 나온 코드를 '목적코드' 라고 부른다.

Java에서는 .java 파일을 컴파일하면 .class 파일이 나오는데, 이 파일은 컴퓨터가 기계어는 아니고, JVM이 이해할 수 있는 *'바이트코드'* 이다.<br>
그러면 JVM은 바이트코드를 보고 다시 컴퓨터가 이해하도록 바꿔주는 작업을 거친다.

> 컴퓨터가 이해하도록 바꿔주지 않더라도 다른 프로그래밍 언어로 바꿔주거나, 사람이 볼 수 있도록 문서나 그림 등으로 바꿔주는 과정 또한 컴파일이라고도 한다.<br>

#### 2-2. interpreter

비슷한 것으로 *interpret*, *interpreter*라는 것도 있는데, 컴파일러가 전체를 해석하여 결과를 한번에 내어준다면, 인터프리터는 한 줄씩 해석해서 해석 결과를 바로바로 전달하는 것이다.<br>
> 실제로 interpreter라는 단어의 뜻 자체도 통역사이다. 대화 중 통역해주는 것을 생각하면 이해하기 쉬울듯..

### 2-3. 컴파일 하고 실행시켜보기

Java로 작성된 파일은 확장자가 *.java*이다.

![compile01](https://user-images.githubusercontent.com/53729311/99221756-8463d180-2824-11eb-9703-d7c9d55a0041.jpg)<br>
일단 메모장을 이용하여 클래스를 하나 만들어 내용을 적은 후 .java라는 이름으로 저장하였다.

![compile02](https://user-images.githubusercontent.com/53729311/99221772-8f1e6680-2824-11eb-9f05-c4dcb4474839.jpg)<br>
이제 java 파일을 저장한 위치에서 명령프롬프트 창을 열어 `javac Compile.java`라고 입력하면 잠시동안 아무 일도 일어나지 않다가 해당 위치에 Compile.class라는 파일이 생기는 것을 볼 수 있을것이다. JVM이 읽을 수 있도록 파일이 바뀐것이다.

![compile03](https://user-images.githubusercontent.com/53729311/99221787-96457480-2824-11eb-88cf-671fe43a6267.jpg)<br>
이제 다시 명령프롬프트에서 `java Compile`이라 입력하니 해당 문서가 실행되어 컴파일을 해보자!라는 문구가 출력되었다.

- .java 문서 작성
- 해당 문서가 있는 위치에서 명령프롬프트에 `javac 문서이름.java` 명령어 입력하여 .class 파일 생성
- 해당 클래스 파일이 있는 위치에서 명령프롬프트에 `java 문서이름` 명령어 입력

> 컴파일러는 어디에..?<br>
> 자바를 설치한 위치의 bin 폴더를 보면 javac.exe라는 프로그램이 있다. 이것이 자바 컴파일러이며, IDE를 사용하게 된다면 지금처럼 직접 명령어를 이용하여 컴파일러를 실행시킬 일은 없겠지만, 컴파일러의 위치는 어디인지, 컴파일을 어떻게하고, 어떻게 실행시키는지 정도는 알아두자.<br>
> 그리고 같은 위치에 java.exe라는 프로그램은 자바파일을 실행시켜준다.

### 2-4. javac의 옵션

2-3에서 javac 명령어를 통해 컴파일을 해보았다. 명령어에는 여러 옵션을 추가할 수 있는데, cmd 창에서 명령어 뒤에 -help라고 붙이면 해당 명령어의 옵션을 확인할 수 있다.

![javac01](https://user-images.githubusercontent.com/53729311/99221809-a2c9cd00-2824-11eb-839f-d0300085f43c.jpg)<br>

전부 보진 않고 몇가지만 살펴보자.<br>
- -cp / -classpath<br>
컴파일 할 때 필요한 라이브러리나 클래스들의 경로를 지정해준다. 컴파일하려는 파일이 외부 라이브러리나 다른 클래스들을 의존하는 중이라면 의존 중인 클래스들의 해당 옵션을 이용하여 필요한 클래스들의 경로를 알려주어야 한다.

- -d<br>
컴파일 하여 나올 클래스 파일을 저장할 위치를 정해준다. 특별히 지정하지 않고 컴파일 한다면 소스파일이 있는 곳에 생긴다.

- -encoding <br>
![javac02](https://user-images.githubusercontent.com/53729311/99221824-a9f0db00-2824-11eb-93f5-ca73071591fb.jpg)<br>
소스파일에 사용된 인코딩을 설정한다. 가끔 파일을 컴파일 하려하면 error가 발생하며 unmappable character for encoding XXX 같은 문구가 뜰때가 있다. 해당 옵션을 이용하지 않고 그냥 컴파일 하게된다면 컴파일러는 플랫폼의 기본 인코딩으로 컴파일 하려한다. 하지만, 소스코드를 저장할 때 지정해준 문자열 인코딩과, 플랫폼의 기본 문자열 인코딩이 다를 경우 위와 같은 에러가 발생하므로 위의 옵션을 사용해서 컴파일해주자.<br>
> 플랫폼이란 개발환경이나 실행황경 등 어떤 목적을 수행할 수 있는 환경을 말한다. 여기서는 운영체제를 뜻한다.

- -g<br>
모든 디버깅 정보를 생성시킨다.

- -nowarn <br>
경고메세지를 생성시키지 않는다.

- -sourcepath <br>
소스파일의 위치를 지정한다.

- -target <br>
자바 버전을 지정하여 컴파일 시킨다. 참고로 상위 버전에서 컴파일 한 클래스 파일은 하위버전의 JVM에서는 실행할 수 없지만, 하위 버전에서 컴파일 한 클래스 파일은 상위버전에서는 실행시킬 수 있다.<br>

<br>

## 3. 바이트코드란?

2-3번에서 컴파일을 해서 JVM이 읽을 수 있도록 .class 파일을 만들었다. 이렇게 고급언어로 작성된 코드를 가상머신이 이해할 수 있도록 컴파일 하여 나온 결과 코드를 *바이트코드*라고 한다.(컴퓨터가 이해하는 기계어와는 다르다.)<br>
이제 JVM은 바이트코드를 읽어 각각의 기기가 이해할 수 있는 기계어로 인터프리터 방식으로 해석해서 프로그램을 실행시켜준다.

그리고 JVM은 Java언어로 작성된 코드를 그대로 읽어 실행시키는 것이 아니라 바이트코드를 읽어서 실행시킨다고 했는데, 반대로 생각하면 어떤 언어로 프로그램을 작성하더라도, 해당 코드를 바이트코드로 컴파일 해줄수만 있다면 JVM을 통해 실행시킬 수 있다는 뜻이다.

## 4. JIT

## 5. JVM의 구성요소

<p><a href="https://commons.wikimedia.org/wiki/File:JvmSpec7.png#/media/파일:JvmSpec7.png"><img src="https://upload.wikimedia.org/wikipedia/commons/d/dd/JvmSpec7.png" alt="JvmSpec7.png" width="80%"></a><br>By <a href="//commons.wikimedia.org/w/index.php?title=User:Michelle_Ridomi&amp;amp;action=edit&amp;amp;redlink=1" class="new" title="User:Michelle Ridomi (page does not exist)"> Michelle Ridomi</a> - <span class="int-own-work" lang="ko">자작</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=35963523">링크</a></p>

### Class Loader

클래스로더는 클래스를 읽어오는 부분인데, 로딩 -> 링크 -> 초기화 순서대로 진행된다.<br>
Runtime 시에 동적으로 클래스들을 읽어오는데(load) 만약 로딩 중 필요한 클래스가 존재하지 않다면, ClassNotFoundException이 발생한다.<br>
이렇게 불러와진 클래스들은 위의 그림에서 JVM Memory 중 Method 영역에 쌓이게 된다.

클래스로더에는 다시 3종류가 있는데, Bootstrap, Platform(Extension), System(Application) ClassLoader가 있다.<br>
System -> Platform -> Bootstrap 순서로 실행되며, 각각 Java 프로그램에 사용되는 클래스파일, 확장 클래스파일, 자바 기본 라이브러리들을 불러온다.
Bootstrap ClassLoader는 환경변수로 설정한 <JAVA_HOME>의 jre/lib/에 위치한 자바 기본 라이브러리들을 불러온다.<br>
Extension ClassLoader는 jre/lib/ext에 위치한 클래스 파일들을 불러온다.<br>
Application ClassLoader는 환경변수에 있는 파일을 불러온다.<br>
> 위의 내용은 정확하지 않다. 이후 다시한번 찾아보자..<br>
> [Baeldung](https://www.baeldung.com/java-classloaders)<br>
> [Java 클래스로더 훑어보기](https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/) by HomoEfficio

### Method Area

메소드, 클래스, static 영역 등 다양한 이름으로 불린다.<br>
JVM이 실행 시 생성되는 공간으로, ClassLoader에 의해 로딩된 클래스의 바이트코드, 클래스 멤버변수, 메서드 등 클래스 수준의 정보가 저장되는 공간이다.
참고로 실행에 필요한 패키지, 클래스가 처음으로 사용될 때 로딩되고, 작성한 모든 클래스가 처음부터 바로 로딩되는 것은 아니다.(궁금하면 static 블록을 이용해서 확인하자)

### Stack 영역

Stack영역은 Java Thread 별로 각각 생성되어 공유할 수 없는 영역으로, 메서드가 호출되면 Stack영역에는 메서드 프레임이 추가(push) 되었다가, 종료되면 제거(pop) 된다.<br>
Stack에 저장되는 메서드 프레임 내부는 지역변수가 저장되는 local variable area와, 임시값이 저장되는 operand stack, 프레임에 대한 정보가 저장되는 frame data로 다시 나뉜다.<br>
스레드가 종료되면 해당 영역은 삭제된다.

### Heap 영역

JVM을 시작할 때 생성되는 영역으로, 객체, 배열, 참조변수의 값, 인스턴스 멤버변수 등이 저장된다.<br>
Garbage Collector이 활동하는 공간으로, 사용하지 않는 메모리는 GC에 의해 삭제된다.<br>
Heap 영역은 다시 세 영역으로 나뉘며 자세한 내용은 [notion](https://www.notion.so/yoonstechstudy/GC-Garbage-Collection-da639a6fc2244eaf9d418ffcae940ec5) 참고..

### PC Registers

스레드가 시작될 때 생성되며 각 스레드별로 하나씩 생성된다.<br>
스레드가 각자 어떤 부분의 어떤 명령을 실행해야 하는지에 대한 기록을 하는 부분으로, 현재 수행중인 JVM 명령의 주소를 가진다.

### Native Method Stacks

자바가 아닌 다른 언어로 작성된 네이티브 코드가 저장되는 영역이다.

### Execution Engine

실행엔진으로 런타임 영역에 배치된 바이트 코드들을 명령어 단위로 읽어서 실행시켜주는 엔진이다.<br>
여기서는 바이트코드를 컴퓨터가 읽을 수 있도록 다시 기계어로 해석하는데, 이때 Interpreter와 JIT 컴파일러가 사용된다.

<br>

## 6. JDK와 JRE

JDK는 Java Devel



<hr>

- 관련 수업

[백기선님의 live-stydy](https://github.com/whiteship/live-study/issues) 1주차

<br>

- 참고

[What is the JVM? Introducing the Java Virtual Machine](https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html), By Matthew Tyson, Java Developer, JavaWorld
