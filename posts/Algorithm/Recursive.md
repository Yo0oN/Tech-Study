---
created: 2022-07-24
modified: 2022-07-24
tags: [Algorithm]
title: Recursive
author: Yo0oN
categories: [Algorithm]
---


# Recursive 재귀 알고리즘

## 재귀?
> 자기가 자기 자신을 호출하는 것

재귀알고리즘은 시간복잡도가 $2^n$이기 때문에 시간이 오래걸린다.
재귀함수를 이용하면 메모리와 시간이 많이 소요되기 때문에 상황에 따라 반복문이나 다이나믹 프로그래밍을 사용하는 것이 더 좋을수도 있다.

![패스트캠퍼스 재귀](https://user-images.githubusercontent.com/53729311/180653021-85460418-1cd9-409f-a092-c71c9b30ced4.png)



#### 예시1. 이진수만들기

```java
class Binary {  
    static StringBuilder result = new StringBuilder();  
  
    public static void main(String[] args) {  
        Binary T = new Binary();  
        T.DFS(11);  
        System.out.println(result.toString());  
    }  
  
    public void DFS(int n) {  
        if (n == 0) return; // n이 0이면 더이상 나머지가 나오지 않는다.  
        else {  
            result.insert(0, n % 2); // 나머지가 2진수를 이룬다.  
            DFS(n / 2); // 남은 몫으로 계속 나머지를 구한다.  
        }  
    }  
}
```


#### 예시2. 팩토리얼

```java
public int factorial(int n) {
	if (n <= 1) {
		return 1;
	}
	return n * factorial(n-1);
}
```


#### 예시3. 피보나치 수열

참고로 코테에서 아래의 코드를 이용하면 보통 시간초과가 뜬다.

```python
def fibo (n):
	if n <= 2:
		return 1
	return f(n - 2) + f(n - 1)
```

```java
public int fibo1(int n) {  
    if (n == 1) return 0;  
    else if (n == 2) return 1;  
    else return fibo1(n - 2) + fibo1(n - 1);  
}
```

한번 나왔던 값들을 저장해두면 시간이 덜 걸린다. 
```java
public int fibo2(int n) {  
    if (fiboArray[n] > 0) return fiboArray[n]; // 이미 구해진 값이면 구해진것 이용
    
    if (n == 1) return fiboArray[n] = 0;  
    else if (n == 2) return fiboArray[n] = 1;  
    else return fiboArray[n] = fibo2(n - 2) + fibo2(n - 1);  
}
```


#### 예시4. 하노이의 탑

```python
def hanoi(n, left, mid, right):
	if n == 1:
		print('boar', n, 'move', from, '->', to)
```