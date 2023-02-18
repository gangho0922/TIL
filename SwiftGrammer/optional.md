# Optional
## 1. 옵셔널이란?
옵셔널은 swift의 특징 중 하나인 안정성을 문법으로 담보하는 기능으로, <br>
값이 있을수도, 없을수도(nil)를 나타내는 표현이다.
## 2. 옵셔널의 사용방법
- 옵셔널은 옵셔널로 선언된 곳에서만 nil을 할당할 수 있다!<br>
(일반 변수나 상수에다가 nil을 할당시킬 시, 컴파일 오류 발생)<br><br>
- 옵셔널 변수 또는 상수 등은 데이터 타입 뒤에 물음표를 붙여 표시해준다. <br><br>
- 함수에서 매개변수를 굳이 넘기지 않아도 될 경우에는 매개변수 타입을 옵셔널로 <br> 정의 할 수 있다.
```swift
var kanghoann: String? = "handsome"
print(kanghoann) // handsome 출력!

kanghoann = nil
print(kanghoann) // nil 
```
## 3. 옵셔널 추출
옵셔널이 아닌 변수에는 옵셔널 값이 들어갈 수 없으므로 추출해서 할당해주어야 한다.
### 강제 추출
- 옵셔널 강제 추출 방식은 런타임 오류가 일어날 가능성이 제일 높은 방법이다.
- 옵셔널의 값을 강제 추출하려면 옵셔널 값의 뒤에 느낌표를 붙여주면 강제로 값을 추출하여 반환 시킨다.
- 강제 추출 시 옵셔널에 값이 없다면, 런타임 오류 발생!
```swift
var animal: String? = "cat"
var mypet: String = animal!

print(mypet) // cat 출력!!

animal = nil
mypet = animal! //런타임 오류 발생!!
```
### 옵셔널 바인딩
- 옵셔널 바인딩은 옵셔널에 값이 있는지 확인할 때 사용한다.
- 옵셔널에 값이 있다면 옵셔널에서 추출한 값을 상수나 변수로 할당해서 사용할 수 있도록 해준다.
- 옵셔널 바인딩은 if 또는 while 구문 등과 결합하여 사용 가능하다.
```swift
var myName: String? = "Kangho"

if let name = myName { //상수에 할당
	print("My name is \(name)")
} else {
	print("myName == nil")
}
//My name is Kangho

if var name = myName { //변수에 할당
	name = "Benjamen"
	print("My name is \(name)")
} else {
	print("myName == nil")
}
//My name is Benjamen
```
### 암시적 추출 옵셔널
- 암시적 추출 옵셔널은 nil을 할당해줄 수 있는 옵셔널이 아닌 변수나 상수를 사용할 때 사용한다.
- 암시적 추출 옵셔널을 사용하려면 타입 뒤에 느낌표를 사용하면 된다.
- 암시적 추출 옵셔널로 지정된 타입은 일반 값처럼 사용할 수 있으나, 옵셔널이기 때문에 nil도 할당할 수 있다.
- nil이 할당되어 있을 때 접근을 시도한다면 런타임 오류가 발생!!
```swift
var myfish: String! = "selfish"
print(myfish) // selfish 출력!!

myfish = nil

if let fish = myfish {
    print("My fish is \(fish)")
} else {
    print("myfish == nil")
}
// myfish == nil 출력 !!
```

이상으로 optional에 대한 소개를 마치도록 하겠다.