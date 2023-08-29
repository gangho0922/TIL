# swift _(underscore)

### underscore란??
이번에는 underscore(_)에 대해서 한번 배워볼건데 이 _는 대체 무엇을 의미할까?<br>
한번 알아보자!!
___
### 1. 함수 인자 label 생략하기
기존 함수를 호출하게 될 때
```swift
function(label: "KangHo")
```
위와 같은 방법으로 호출하게 될텐데 여기서 !
```swift
func function(_ name: "KangHo") {
    print("I'm \(name)")
}

function("KangHo")
```
label 앞에 _를 추가하게 된다면 함수 호출 시에 label을 생략할 수 있다!!
___
### 2. 반복문 파라미터 생략하기
만약 반복문의 파라미터를 사용하고 싶지 않다면
```swift
for _ in 1...10 {
    print("Hi")
}
```
위와 같이 _를 사용해서 생략 시킬 수 있다!
___
### 3. tuple의 구성요소를 무시한다!
```swift
let tuple1 = (1, 2, 3, 4, 5)
```
위와 같은 tuple이 있다고 가정할 때 

#### 여기서!!!

만약 5가 필요없다고 가정한다면
```swift
let (a, b, c, d, _) = tuple1

print(a, b, c, d) //1 2 3 4 출력
```
이런식으로 필요하지 않는 요소를 _를 통해서 무시할 수 있다!

### 추가로!
switch문 같은 경우에도 tuple이 쓰일텐데 이와 같은 경우도
```swift
case(_ , 5):
```
이런식으로 무시가 가능하다!!
___

### 4. 숫자의 가독성?
```swift
1000000
```
이런식의 숫자가 있다고 가정할 때

```swift
1_000_000
```
이렇게 보기 좋게해서 가독성을 높일 수 있다!!
___

### 5. 함수 반환 값을 생략한다!
```swift
func age() -> Int {
    return 100
}
```
이런 함수가 있다고 가정할 때 반환값을 버려버릴수도 있겠지만

```swift
_ = age()
```
_를 사용해서 반환 값이 필요없다는 것도 강조할 수 있다.

___

이상으로 underscore에 대한 공부를 마치도록 하겠다.