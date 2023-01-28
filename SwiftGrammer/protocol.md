# Protocol
프로토콜이란?<br>
특정 역할을 하기 위한 메소드, 프로퍼티, 기타 요구사항 등의 청사진이다.
### Protocol의 사용
- 구조체, 클래스, 열거형은 프로토콜을 채택해서 특정 기능을 실행하기 위한 프로토콜의 요구사항을 실제로 구현할 수 있다.
- 프로토콜은 정의를 하고 제시를 할 뿐 스스로 기능을 구현하지 않는다.(조건만 정의한다.)
- 하나의 타입으로 사용되기 때문에 아래와 같이 타입 사용이 허용되는 모든 곳에 Protocol을 사용할 수 있다.
  >-함수, 메소드, initializer의 파라미터 타입 또는 리턴타입<br>
  >-상수, 변수, 프로퍼티의 타입<br>
  >-배열, 딕셔너리의 원소타입
## 1. 기본 형태
```swift
protocol 프로토콜의 이름 {
    // 프로토콜 정의
}
```
구조체, 클래스 열거형 등에서 protocol을 채택하려면 타입 이름 뒤에 ":"을 붙여준 후,<br> 채택할 protocol 이름을 ","로 구분하여 명시해준다.(SubClass일 경우 SuperClass를 가장 앞에 명시한다.)
```swift
struc Some Struct: AProtocol, AnotherProtocol {
    //구조체 정의
}
//상속받는 클래스의 프로토콜 채택 방법
class SomeClass: SuperClass, AProtocol, AnotherProtocol {
    //클래스 정의
}