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

> JVM - Java Virtual Machine

JVM은 자바 프로그램을 실행시키도록 해주는 가상머신, 프로그램으로 크게 두가지 기본 기능이 있다.(JVM의 구성 요소는 아래쪽에..)

### ***Write once, run anywhere***

Java 언어를 설명하기 위한 슬로건으로, Java로 작성된 프로그램은 한번 작성하면 어느 장치, 운영체제에서나 실행 가능하도록 해주는 언어라는 것을 뜻한다.~~(Write Once, Debug Everywhere)~~

처음 자바를 사용하기 전 컴퓨터 프로그램들은 같은 프로그램이어도 여러 운영체제에 맞춰 다르게 작성해야 했다.
그런데 1995년 등장한 Java는, 프로그램을 한 번만 작성하면 Java 프로그램과 운영체제 사이에서 JVM이 동작하여 운영체제, CPU등에 관계없이 동일하게 Java 프로그램이 동작하도록 해주었다.<br>
초기에는 Java 프로그램이 JVM 위에서 작동하기 때문에 빠르지 못하다는 이유로 C에 비해 

### Garbage Collection

어떤 언어들은 프로그래머가 해당 프로그램의 메모리 관리를 모두 해야한다.<br>
하지만 JVM은 Java 프로그램에서 사용하지 않는 메모리를 식별하고, 사용하지 않는다면 제거해주는 Garbage Collection 프로스세스를 통해 메모리 관리를 대신 해준다.

<br>

## 2. 컴파일 방법

### Compile?

컴파일은 특정 프로그래밍 언어로 작성된 문서를 다른 프로그래밍 언어로 옮기는 과정을 말한다.


IDE를 이용하는 경우는 IDE가 알아서 컴파일을 해준다.



<hr>

- 관련 수업

[백기선님의 live-stydy](https://github.com/whiteship/live-study/issues) 1주차

<br>

- 참고

[What is the JVM? Introducing the Java Virtual Machine](https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html), By Matthew Tyson, Java Developer, JavaWorld
