# Generic
## Generic이란?
제네릭이란 타입에 의존하지 않는 범용 코드를 작성할 때 사용한다
제네릭을 사용하면 중복을 피하고, 코드를 유연하게 작성할 수 있다.

그런데 generic이란 대체 무엇이고 대체 언제 사용할까?

지금 한번 알아보자!
___
### Generic 함수
우리가 만약에 인자로 오는 두 Int형 타입을 스왑하는 함수를 만들고 싶다면
```swift
func swapTwoInts(_ a: inout Int, _b: inout Int) {
    let t = a
    a = b
    b= t
}
```
이런식으로 짤 수 있을 것이다. 근데 위 파라미터 같은 경우 모두 Int형일 땐 잘 돌아가지만 만약 타입이 double이나 string일 경우엔 사용할 수 없게 된다.

만약 double이나 string을 사용하고 싶다?

그러면...
```swift
func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
    let t = a
    a = b
    b = t
}// double형 타입.

func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let t = a
    a = b
    b = t
}// String형 타입.
```
이런식으로 각각의 타입(형식)에 맞춰서 함수를 오버로딩을 할 수도 있다.

하지만 이렇게 하면 코드도 복잡해지고 개발자 입장에서도 많이 귀찮음을 느끼게 할 수도 있다.

### 그래서!!!!
이때를 위해서 준비한게 바로 genericd이다!!

generic은 타입에 제한을 두지 않는 코드를 사용하고 싶을 때 사용한다.
```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let t = a
    a = b
    b = c
}
```
이런식으로 사용하게 된다.
<> 를 이용해서 안에 타입처럼 사용할 이름을 선언해주면 그뒤로 해당이름을 타입처럼 사용할 수 있다!!

위 코드에서 이 T를 Type parameter라고 부르는데 T라는 새로운 형식이 생성되는 것이 아니라, 실제 함수가 호출될 때 해당 매개변수의 타입으로 대체되는 placeholder이다.

<>로 사용할 이름을 감싸는 이유는 위에서 말했듯이 <>안에 사용할 이름은 새로운 형식이 아닌 placeholder이기 때문에 실제로 이 타입의 존재여부를 따지지 않게 하기 위해서 <>로 감싸는 것이다.

```swift
var someInt = 1
var otherInt = 2
swapTwoValues(&someInt, &otherInt)

var someString = "storyboard"
var otherString = "database"
swapTwoValues(&someString, &otherString)
```
이렇게 실제 함수를 호출할 때 type parameter인 T의 타입이 결정되는 것이다.

근데 여기서 파라미터 a,b 모두 같은 타입 파라미터인 T로 선언되어 있기 때문에 
```swift
swapTwoValues(&someInt, &otherString)// 안됨!!
```
이런식으로 서로 다른 타입을 파라미터로 전달하게 된다면, 첫번째 someInt를 통해 타입 파라미터 T가 Int로 정해졌기 때문에 두번째 파라미터인 otherStrings의 타입이 Int가 아니라고 에러가 발생하는 것이다.
```swift
func swapTwoValues<One, Two> {...}
```
타입 파라미터는 굳이 T가 아닌 원하는 이름으로 마음대로 바꿔도 되고, 한개 말고 여러 개의 (,)를 사용해서 선언할 수도 있다.

우리가 T로 파라미터를 선언하는 이유는 보통 가독성을 위해서 T 같은 단일 문자나 Upper Camel Case를 사용한다고 한다.
___
### generic type
generic은 함수에만 사용이 가능한 것이 아닌 struct, class, enum 타입에도 선언할 수 있다.

이것을 보고 **generic type** 이라고 한다!

만약 Stack을 generic으로 만들고 싶다면...
```swift
struct Stack<T> {
    let items: [T] = []

    mutating func push(_ item: T) {...}
    mutating func pop(_ item: T) {...}
}
```
이런식으로 generic을 사용해서 선언가능!!!(클래스, 열거형도 ==)

그럼 generic type의 인스턴스를 생성할려면?
```swift
let stack1: Stack<Int> = .init()
let stack2 = Stack<Int>.init
```
이렇게 generic type을 선언할 땐, 선언과 마찬가지로 <>를 통해서 어떤 타입으로 사용할 것인지 명시해줘야 된다!!

```swift
let array1: Array<Int> = .init()
let array = Array<Int>.init()
```
이건 배열 생성 할때의 타입선언이다.

위랑 아래랑 좀 비슷하다고 생각하지 않나??

왜냐하면 그 이유는...
```swift
@frozen public struct Array<Element> {

}
```
Swift에서는 Array가 바로 generic type이기 때문!!
___
## type constraints
generic 함수나 타입을 사용할 때 특정 클래스의 하위 클래스나, 특정 프로토콜을 준수하는 타입만 받을 수 있게 제약을 둘 수 있다!
___
### protocol constraints
만약 우리가 파라미터로 두개의 값을 받은 후 두 값이 같으면 true 아니면 false를 반환하는 함수를 generic으로 선언하려고 한다면...
```swift
func isSameValues<T>(_ a: T, _ b: T) -> Bool {
    return a == b
}
```
이렇게 선언하면 될 것 같지만... 

== 연산자는 a와 b의 타입이 Equatable이란 protocol을 준수할 때만 사용할 수 있다.

T라고 선언한 파라미터는 a,b가 Equatable protocol을 준수하는 타입인지 아닌지 알 수 없기 때문에 == 연산자를 쓰면 안되는 것이다.

따라서,
```swift
func isSameValues<T: Equatable>(_ a: T, _ b: T) -> Bool {
    return a == b
}
``` 
다음과 같이 타입 파라미터에 제약을 줄때는 **T: Equatable** 이런 식으로 제약을 줄 수 있다.

이런 식으로 제약을 주게 되면 Equatable이란 프로토콜을 준수하는 파라미터만 받을 수 있게 된다.
___
### class constraints
클래스 제약 같은 경우 프로토콜 제약과 같지만, 프로토콜이 아니라 클래스 이름을 넣어주는 것이 포인트다.

```swift
class Cat {}
class Person {}
class Policer: Person {}

func Name<T: Person>(_ a: T) {}
```
이렇게 generic을 써주면
```swift
let cat = Cat.init()
let person = Person.init()
let policer = Policer.init()

Name(cat)
Name(person)
Name(policer)
```
Person 클래스의 인스턴스인 person과 Person 클래스를 상속 받은 policer는 Name이란 generic 함수를 실행시킬 수 있지만 Person 클래스를 상속 받지 않은 cat 인스턴스는 실행 할 수 없다...
___
## generic 확장시키기
만약에 generic type인 Array를 내가 확장 시키고 싶다면
```swift
extension Array {
    mutating func pop() -> Element {
        return self.removeLast()
    }
}
```
generic type을 확장시키면서 type parameter를 사용할 경우, 실제 Array 구현하는 부분에서 type parameter가 Element이기 때문에 따라서 Element를 사용해야 한다.
```swift
extension Array<T> {}

extension Array {
    mutating func pop() -> T {
        return self.removeLast()
    }
}
```
확장에서 새로운 generic을 선언하거나 다른 type parameter를 사용하면

### 안된다!!

where을 통해서 확장에 제약을 줄 수 있는데
```swift
extension Array where Element: FixedWidthInteger {
    mutating func pop() -> Element { return self.removeLast() }
}
```
위와 같이 type parameter인 Element가 FixedWidthInteger라는 protocol을 준수해야 된다는 제약 조건을 준다면..
```swift
let numbers = [1,2,3,4]
let strings = ["k","a","n","g","h","o"]

numbers.pop() 
strings.pop() // X
```
FixedWidthInteger라는 Protocol을 준수하는 Array<Int> 형인 numbers는 extension에서 구현된 pop이라는 메서드를 활용할 수 있지만..

저 protocol을 준수하지 않는 Array<String> 형인 strings는 extension에서 구현된 Pop이라는 메서드를 활용할 수 없다!
___
## generic 함수의 오버로딩
generic 말고 다른 함수로 구현을 하고 싶다면 이땐 generic함수를 오버로딩을 하면 된다.
```swift

func swapValues<T>(_ a: inout T, _ b: inout T) {
    print("generic")
    let temp = a
    a = b
    b = temp
}
 
func swapValues(_ a: inout Int, _ b: inout Int) {
    print("specialized")
    let temp = a
    a = b
    b = temp
}
```
이렇게 했을 경우에 타입이 지정된 함수가 제네릭 함수보다 우선 순위가 높기 때문에
```swift
var a = 1
var a = 10
swapValues(&a, &b) //"specialized"

var c = "Hi"
var d = "Hello"
swapValues(&c, &d) //"generic"
```
Int형으로다가 swapValues를 실행하면 타입을 지정된 함수로 실행이 되게 되고,<br><br>
String형으로다가 swapValues를 실행하면 String 타입으로 지정된 함수가 없기 때문에 generic 함수가 실행되게 된다.

___
이상으로 generic에 대한 공부를 마치도록 하겠다.