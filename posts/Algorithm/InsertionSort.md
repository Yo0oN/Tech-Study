---
created: 2020-07-04
modified: 2020-07-04
tag: [Algorithm, Sort]
title: Insertion Sort
author: Yo0oN
category: Algorithm
---

## 1. 삽입정렬

배열의 0번 원소를 기준으로 하여 뒤의 1번 원소부터 앞과 비교하여 앞의 값보다 크면 그자리, 작으면 앞에 끼워넣는다.<br>
0번과 1번은 정렬되어있는 상태로, 2번 원소를 다시 앞의 값들과 비교하여 제자리에 삽입한다.

![01](https://user-images.githubusercontent.com/53729311/180646266-0db234d1-1e73-4f50-9725-08f1c14cbb38.gif)

마치 카드게임에서 카드를 이동시키는것과 비슷하다.

![02](https://user-images.githubusercontent.com/53729311/180646268-69642f16-0c28-451d-8cc5-031c9031d9eb.png)

또한 삽입정렬은 동일한 수가 있을 경우 자리가 바뀌지 않는 안정(stable)정렬이다.

![03](https://user-images.githubusercontent.com/53729311/180646270-1755224f-7504-41b7-82c2-39504ad6c7bc.jpg)

<br>

### 1-1. 복잡도

첫번째 비교시에는 한번만 비교하므로 1,<br>
두번째는 2, 세번째는 3... 마지막에는 n-1번 비교를 하게 된다.
모두 더하면 1 + 2 + ...(n - 1)이 된다.

그래서 선택정렬의 시간복잡도는 O(n^2)이 된다.
운이 좋아 한번의 비교만으로 정렬이 끝나는 최선의 경우 복잡도는 Ω(n)이다.

또한, 삽입정렬은 하나의 배열 안에서 정렬이 이루어지기 때문에 공간복잡도는 O(n)이다.

<br>

## 2. 구현하기 - python

```python
def insertionSort(list) :
  for pivot in range(1, len(list)) :
    for index in range(pivot, 0, -1) :
      if list[index] < list[index - 1] :
        list[index], list[index - 1] = list[index - 1], list[index]
      else :
        # 만약 두 수의 자리가 바뀌지 않았다면 해당 차수의 정렬이 끝난것이다.
        # 더이상 확인하지 않고 다음 순서로 넘어간다.
        break
```
