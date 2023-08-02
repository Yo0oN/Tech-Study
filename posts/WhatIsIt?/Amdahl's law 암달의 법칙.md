---
tags: [ComputerScience, WhatIsIt?]
title: Amdahl's law 암달의 법칙
author: Yo0oN
categories: [WhatIsIt?]
---


## Amdahl's law

처음 알게된 것은 Java 성능튜닝 책을 읽다가 본 것으로 기억한다.
<br>
>컴퓨터 시스템의 일부를 개선할 때 일부 작업 시간을 절대 개선할 수 없다면 전체 작업 속도는 더 이상 향상시킬 수 없다.
<br>
컴퓨터 시스템의 일부를 개선할 때 전체적으로 얼마만큼의 최대 성능 향상이 있는지 계산하는 식이 있다.

$$성능 개선율 = \frac{1}{(1 - P) + \frac{P}{S}}$$
예를들어 전체 작업 시간 중 10%(P)를 차지하는 작업의 속도를 2배(S) 증가시켰다면 전체 작업 속도는 약 1.05배 증가한다.
<br>
그런데 아무리 증가시키더라도 특정 작업 시간에 대해서는 절대 개선할 수 없다면, 전체 작업 속도는 더 이상 향상시킬 수 없다.
<br>
아래의 그림이 해당 내용을 나타낸다.

![Amdahl's law](https://github.com/Yo0oN/CodingTestStudy/assets/53729311/ecf1d16b-85ee-4859-8f86-0457b2e6c3d1)
[그림 출처](https://ko.wikipedia.org/wiki/%EC%95%94%EB%8B%AC%EC%9D%98_%EB%B2%95%EC%B9%99#/media/%ED%8C%8C%EC%9D%BC:AmdahlsLaw.svg)
<br>
이렇게 일부 작업 시간을 절대 개선할 수 없다면 전체 작업 속도는 더 이상 향상시킬 수 없는데, 이때문에 암달의 저주라고도 불린다.