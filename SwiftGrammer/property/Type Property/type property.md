# Type Property
### 먼저 Computed Property 부분을 먼저 보고 와주세요!
다음으로 설명할 것은 타입 프로퍼티에 대해서 알아볼건데요.
___
## 타입 프로퍼티(Type Property)란?
저장 프로퍼티와 연산 프로퍼티의 형태가 존재하며 저장 프로퍼티의 경우 선언할 때 원하는 값으로 항상 초기화 되있어야 한다.
**static** 을 이용해서 선언하며, 자동으로 lazy로 되서 lazy를 굳이 붙일 필요는 없다.<br>
### 쓰이는 경우
* 클래스
* 구조체
* 열거형

간단하게 말하자면 그냥 저장 프로퍼티나 연산 프로퍼티 앞에다가 **static** 을 붙인게 **저장 타입 프로퍼티** 혹은 **연산 타입 프로퍼티**가 되는 것이다.
```swift
class Human {
    let name: String = "kangho" // 저장 프로퍼티
    var babo: String { //연산 프로퍼티
        return name + "는 바부"
    }
}
```
위과 같은 저장 프로퍼티와 연산 프로퍼티가 들어가 있는 코드에다가 다음과 같이
```swift
class Human {
    static let name: String = "kangho" // 저장 프로퍼티
    static var babo: String { //연산 프로퍼티
        return name + "는 바부"
    }
}
```
저장 타입 프로퍼티와 연산 타입 프로퍼티가 되는 것이다.

앞서 저장 프로퍼티는 항상 초기화 되있어야 한다고 했다.<br>
위의 코드와 같이 값을 초기화해 두면 상관이 없는데 만약에
```swift
static let name: String
```
이렇게 두면 어떻게 될까?

static으로 선언할 경우 이니셜라이져가 필수라고 하거나 getter/setter를 지정해달라는 오류가 발생하게 된다.

위의 에러가 잘 이해 안될 수도 있는데 정리해서 말하자면...<br>
```
저장 프로퍼티를 쓰고 싶다면 초기 값을 지정해주고 아니라면 연산 프로퍼티로 바꿔라!
```
이 말이다 그냥ㅎ

저장 프로퍼티를 static으로 초기화 하는 경우 값을 할당하는 이니셜라이져가 없기 때문에 오류가 발생하는 것이다.
___
## 타입 프로퍼티의 접근 방법
```swift
Human.name ~~~
```
이렇게 타입이름을 통해서만 접근이 가능하다.

인스턴스가 생성됐다고 해서 계속해서 생성되는 형태가 아니라, 어디서든 해당 프로퍼티를 공유할 수 있는 형태이다.

인스턴스 생성 시 불리는 이니셜라이져 또한 상관이 없어서 초기값이 없을 경우, 초기 값을 세팅할 방법이 없기 때문에 반드시 초기값을 지녀야 한다.

그리고 타입 프로퍼티의 경우 lazy 속성이기 때문에 name이라는 프로퍼티가 처음으로 호출되기 전까지는 저어얼대!! 초기화 되지 않는다.

```swift
Human.name
```
이렇게 했을 경우 메모리가 올라가서 초기화 되는 것이다.

그런데 지연 저장 프로퍼티의 경우에는 항상 var로 초기화 했어야 했는데 static의 기본이 lazy 동작인데도 let/var로 선언해도 문제 없는 이유는 

타입 프로퍼티는 인스턴스 프로퍼티처럼 초기화 구문의 영향을 받지 않지 않는다.<br> 인스턴스가 초기화 즉 init 함수가 불리든 말든 타입 프로퍼티와는 상관 없다.<br>
따라서 타입 프로퍼티의 경우 초기화 구문에서 값이 없음으로 초기화 되지 않고, 실제 사용할 때 값이 초기화 되기 때문에 let으로 선언해도 문제가 없는 것이다.
___
이미 말했을지 모르겠는데 타입 프로퍼티의 경우 타입 이름에 .을 붙여서 접근한다.
```swift
class Human {
    static var name = "kangho"
    static let age = 18
}
 
Human.name                  // "kangho"
Human.name = "junho"
Human.name                  // "junho"
 
Human.age = 19 // error!    
```

var을 사용하면 수정도 가능하지만 let 즉, 상수의 경우 수정이 불가하다..
___
## 연산 타입 프로퍼티의 오버라이딩
연산 타입 프로퍼티는 Subclass 에서 오버라이딩이 가능하다. 앞에다가 class를 붙이나 static을 붙이냐의 차이이다.

### class : 오버라이딩이 가능한 **연산프로퍼티**
```swift
class Human {
    class var name: String {
        return "Human"
    }
}
 
class Kanghoo: Human {
    override class var name: String {
        return "kangho"
    }
}
 
Human.name             // "Human"
Kanghoo.name            // "kangho"
```
위와 같이 class로 선언 했을 경우 static선언과 마찬가지로 연산 프로퍼티이다!!

Subclass에서 위처럼 연산 타입 프로퍼티를 오버라이딩을 해서 사용할 수 있다!!

### class : 오버라이딩이 불가능한 **연산프로퍼티**
```swift
lass Human {
    static var name: String {
        return "Human"
    }
}
 
class Kanghoo: Human {
    override static var name: String { // error!!
        return "kangho"
    }
}
```
static 프로퍼티는 오버라이딩이 불가능하다면서 에러가 발생한다!!

따라서!!!

사용불가 ㅎ