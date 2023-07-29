# zip
### zip이란?
배열에서 사용하는 결합 연산자로, 두 원소가 항상 같이 짝을 짓는 연산자라고 할 수 있다.
```swift
var ar = [1, 2, 3, 4, 5]
var ray = ["A", "B", "C", "D", "E"]

zip(ar, ray)
    .forEach { value1, value2 in
        print(value1, value2)
    }
```
이런식의 코드가 있다고 하면

![](zip(1).png)

두 원소가 짝이 맞다면 
```
1 A
2 B
3 C
4 D
5 E
```
이런식으로 출력되게 될 것이고,

```swift
var ar = [1, 2, 3, 4, 5]
var ray = ["A"]
```
이렇게 짝이 안맞으면
![](zip(2).png)

이렇게 짝이 맞는 것만 연결되서
```
1 A
```
이렇게만 따로 출력되게 될 것이다.
___
이상으로 zip에 대한 소개를 마치도록 하겠다.