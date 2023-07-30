# merge와 merging
이것들은 dictionary에서 사용하는 병합 연산자로, merge는 인스턴스의 메소드이고, merging은 함수라고 보면 된다.<br>
merge는 직접 인스턴스의 값에 적용을 시키고 merging은 결과값을 리턴하는 기능이다. 클로저로 key값이 겹칙 때 어떤 value를 선택할지 결정이 가능하다.

## 예제
### merge
```swift
var array1 = [1 : "A", 2 : "B"]
var array2 = [2: "C", 3 : "D"]
array1.merge(array2) { _, value2 in 
    value2
}

print(array1)
```
위와 같이 merge를 사용한 코드가 있는데

![](merge(1).png)
이렇게 둘이 겹치는 것을 볼 수가 있다. 하지만 value2를 선택했기 때문에 
![](merge(2).png)
이런식으로 곂치지 않는 걸 먼저 넣고 곂치는 것 중 고른 value2 값을 넣어서
```
[1: "A", 3: "D", 2: "C"]
```
이런식으로 출력시킨다.
___
### merging
```swift
var array3 = [1 : "A", 2 : "B"]
var array4 = [2: "C", 3 : "D"]
let newArray = array3.merging(array4) { value1, _ in 
    value1
}

print(newArray)
```
이번엔 위와 같이 merging을 사용한 코드가 있는데
![](merging(1).png)
이런식으로 이번에도 2가 곂치는 걸 볼 수가 있는데
근데 여기서는 value1을 선택하였기 때문에
![](merging(2).png)
이렇게 선택당한 C를 먼저, 그 다음 순서인 D 마지막으로 A순으로 출력해서
```
[2: "B", 3: "D", 1: "A"]
```
이렇게 출력되게 된다.
___
이상으로 merge와 merging에 대한 공부를 마치도록 하겠다.