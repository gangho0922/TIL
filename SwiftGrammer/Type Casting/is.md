# Type Casting / Is
## 타입 캐스팅이란?
인스턴스의 타입을 확인하거나 해당 인스턴스를 슈퍼 클래스나 하위 클래스로 취급하는 방법이다.

Swift의 타입 캐스팅 연산자
* is
* as

먼저 is에 대해서 알아보자.
___
## is
```swift
표현식 is Type
```
is는 타입을 체크하는 연산자로 런타입 시점에 체크가 이루어진다.

표현식이 Type과 동일하거나 표현식이 Type의 서브 클래스인 경우에 true를 반환시키고, 그 외에는 모두 false를 반환시킨다.

그러므로 반환 값은 Bool형이다.
```swift
let ch: Character = "a"
ch is Character // true
ch is Int // false

let bo: Bool = false
bo is Bool // true
bo is String // false
```
위와 같이 내가 원하는 타입인지 확인하고 싶을 때 사용할 수 있다.

그리고 표현식의 Type의 **서브 클래스**인 경우에도 true를 반환 시키는데 한번 예시를 봐보자.
```swift
class Son {}
class Mom: Son {}

let mom: Mom = .init()
mom is Mom // true
mom is Son // true
```
위와 같이 Son이라는 클래스를 Mom이라는 클래스가 상속 받을 때 mom이라는 인스턴스가 Son클래스의 서브 클래스이기 때문에 이런 경우에는 타입 체크를 하게되면 true를 반환시키게 되는 것이다.
```swift
class Son {
    let name: String
    init(name: String) {
        self.name = name
    }
}

class Mom: Son {}
class Dad: Son {}

let family: [Son] = [
    Mom.init(name: "우리엄마")
    Dad.init(name: "우리아빠")
    Dad.init(name: "큰아빠")
]
```
위와 같이 Son이라는 클래스가 존재하고 이 Son이라는 클래스를 상속받는 서브클래스인 Mom과 Dad가 있다.

그리고 family라는 배열 안에 Mom 인스턴스 1개, Dad 인스턴스 2개를 담았다고 가정하자.

```swift
for son in family {
    if son is Mom {
        print("\(son.name)")
    }
    else if son is Dad {
        print("\(son.name)")
    }
}
```
이렇게 타입 캐스팅을 통해서 확인을 할 수가 있다.

그럼 결과는 
```swift
우리엄마
우리아빠
큰아빠
```
이렇게 나올 것이다.
___
다음으론 as에 대해서 알아보겠다.