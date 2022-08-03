---
created: 2022-08-02
modified: 2022-08-02
tag: [Algorithm]
title: Dynamic Programming and Divide and Conquer
author: Yo0oN
category: [Algorithm]
---

# 동적계획법과 분할 정복

## 동적계획법

> 크기가 작은 문제들을 먼저 해결한 후, 해당 결과를 활용해서 큰 크기의 문제를 해결해 나가는 알고리즘

Memorization(프로그램 실행 시 이전에 계산한 값을 저장하여 다시 계산하지 않도록 하여 실행 속도를 빠르게 하는 기술)을 이용한다.

상향식 접근법으로 최하위의 답을 구하고, 이를 이용하여 상위의 답을 구해나간다.


#### 피보나치 수열

동적 계획법의 가장 대표적인 문제이다.

```Python
def fibo(num):
	cache = [0 for index in range(num + 1)]
	cache[0] = 0
	cache[1] = 1
	
	for index in range(2, num + 1):
		cache[index] = cache[index - 1] + cache[index - 2]
	
	return cache[num]
```



## 분할 정복

> 문제를 나눌 수 없을 때까지 나누어서 각각 푼 후 다시 합쳐서 답을 얻는 알고리즘

하향식 접근법으로 상위의 해답을 구하기 위해 하위의 해답을 구하는 방식인다.
(1번 문제를 풀려고하니 2번 문제를 풀어야해서 2번 문제를 풀게되고, 2번 문제를 풀려고하니 3번문제를 풀어야하는 식.
상향식 접근법과는 좀 다르다.)

보통 재귀함수를 많이 이용한다.


## 동적계획법과 분할 정복의 차이?

- 공통점
	- 문제를 잘게 쪼개서 가장 작은 단위의 문제로 분할
- 차이점
	- 동적계획법
		- 부분 문제는 중복되어, 상위 문제 해결 시 재활용됨(Memorization 기법 사용)
	- 분할 정복
		- 부분 문제는 서로 중복되지 않음


