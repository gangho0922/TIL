# closure
## 클로저란?
클로저는 사용자의 코드 안에서 전단되어 사용할 수 있는 
<br>로직을 가진 중괄호 "{}"로 구분된 코드블록이며, 
<br> 일급 객체의 역할을 할 수 있다.
<br><br>⭐️ 여기서 상식 !!
<br> 일급 객체 : 전달 인자로 보낼 수 있고, 변수, 상수 등으로 저장하거나, <br>
전달할 수 있으며, 함수의 반환 값이 될 수도 있는 객체이다.

클로저는 참조타입이다.

함수는 클로저의 한 형태로, 이름이 있는 클로저라고 할 수 있다.

## 클로저의 표현 방식
```swift
{ (인자들) -> 반환타입 in 
    로직 구현
}
```
아래와 같이 함수로 따로 정의된 형태가 아닌 인자로 들어가 있는 형태의 클로저를 **Inline Closure**라고 한다.
```swift
let reverseNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 >s2})
```
## 클로저의 축약
### 타입 생략
```swift
let reverseNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 >s2})
```
위의 예제에서 sorted(by:)의 경우는 이미 (String, String) -> Bool 타입의 인자가 들어와야 하는지 알고 있기 때문에 클로저에서 타입을 명시하는 것을 생략할 수 있다.
```swift
let reverseNames = names.sorted(by: {s1, s2 in return s1 > s2})
```
하지만 코드의 모호성을 피하기 위해 타입을 명시하는 것이 좋을때도 있다.
### 인자이름 생략
인자 값을 축약해서 사용할 수 있다.(인자의 표기는 $0부터 순서대로)
```swift
let reverseNames = names.sorted(by: {$0 > $1})
```
### 연산자 메소드
연산자를 사용할 수 있는 타입의 경우 연산자만 남길 수 있다.
```swift
let reversedNames = names.sorted(by: > )
```
### 후행 클로저
인자로 클로저를 넣기가 길다면 후행 클로저를 사용하여 함수의 뒤에 표현할 수 있다.
```swift
let reversedNames = names.sorted() {$0 > $1}
```
함수의 마지막 인자가 클로저이고, 후행 클로저를 사용하면 괄호 "()"를 생략할 수 있다.
```swift
let reversedNames = names.sorted { $0 > $1 }
let reversedNames = names.sorted { (s1: String, s2: String) -> Bool in return s1 > s2 }
// 둘이 같음
```
### 값 캡쳐
클로저는 특정 문맥의 상수나 변수의 값을 캡쳐할 수 있다.
<br>즉, 원본 값이 사라져도 클로저의 body 안에서 그 값을 활용할 수 있다.


<br> 다음은 Swift에서 값 캡쳐를 하는 가장 단순한 형태에 대한 예시이다.
```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
  var runningTotal = 0
  func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
  }
  return incrementer
}

let plusTen = makeIncrementer(forIncrement: 10)
let plusSeven = makeIncrementer(forIncrement: 7)

// 함수가 각기 실행되어도 실제로는 변수 runnigTotal과 amount가 캡쳐되서 그 변수를 공유하기 때문에 누적된 결과를 가진다.
let plusedTen = plusTen() // 10
let plusedTen2 = plusTen() // 20
// 다른 클로저이기 때문에 고유의 저장소에 runningTotal과 amount를 캡쳐해서 사용한다.
let plusedSeven = plusSeven() // 7
let plusedSeven2 = plusSeven() // 14
```
plusTen, plusSeven이 상수이지만 runningTotal을 증가시킬 수 있었던 이유는 클로저가 참조타입이기 때문이다.

함수와 클로저를 상수나 변수에 할당할 때 실제로는 상수와 변수에 해당 함수나 클로저의 참조가 할당된다. 만약 한 클로저를 두 상수나 변수에 할당하면 그 두 상수나 변수는 같은 클로저를 참조하고 있게 되는 것이다.

## Escaping Closure
클로저가 함수의 인자로 전달되지만 함수 밖에서 실행되는 것(함수가 반환된 후 실행되는 것)을 Escape한다고 하며, 이러한 경우 매개변수의 타입 앞에 @escaping이라는 키워드를 명시해야한다. 다음과 같은 경우에 자주 사용된다.

## AutoClosure
자동 클로저는 인자 값이 없으며 특정 표현을 감싸서 다른 함수에 전달 인자로 사용할 수 있는 클로저를 말한다. 자동 클로저는 클로저를 실행하기 전까지 실제 실행이 되지 않는다. 즉 실제 계산이 필요할때 호출이 되기 때문에 계산이 복잡한 연산을 하는데 유용하다.

## 고차함수
함수의 인자로 다른 함수를 받는 함수
* 순수 고차함수는 map, filter, reduce를 예로 들 수 있다.
* 고차 함수를 사용하면 변수로 지정할 필요 없이 상수로 지정해서 변환할 수 있다.

**map**
<br> 콜렉션 내부의 기존 데이터를 변형하여 새로운 콜렉션 생성
```swift
let numbers: [Int] = [2,8,15]
var newNumbers: [Int] = numbers.map { $0 + 1 } // [3, 9, 16]
```
**filter**
<br> 콜렉션 내부의 데이터를 조건에 맞는 새로운 콜렉션으로 생성
```swift
let numbers: [Int] = [2,8,15]
var newNumbers: [Int] = numbers.filter { $0 % 2 == 0} // [2, 8]
```
**reduce**
<br> 컨테이너 내부의 콘텐츠를 하나로 통합(ex. Element들의 총합, 총곱 등)
```swift
let numbers: [Int] = [2,8,15]
// 초기값이 3에 정수 배열의 모든 값을 더한다.
var sum: Int = numbers.reduce(3) { $0 + $1 } // 28
```

이상으로 클로저에 대한 소개를 마치도록 하겠다.