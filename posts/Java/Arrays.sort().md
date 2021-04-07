## Java에서의 정렬

Arrays에는 sort()라는 메서드가 있다. 해당 메서드는 배열을 정렬하는데 사용되며, 내부를 보면 DualPivotQuicksort를 이용중이다.

![image](https://user-images.githubusercontent.com/53729311/113885761-12078400-97fb-11eb-9206-29da7e301c70.png)

DualPivotQuicksort에는 3가지 정렬방식이 있는데, 삽입정렬, 병합정렬, 퀵정렬이다.<br>
정렬을 원하는 배열의 크기에 따라 세가지를 골라서 사용하는데, 최근에는 정렬을 섞어서 사용한다고 한다.
