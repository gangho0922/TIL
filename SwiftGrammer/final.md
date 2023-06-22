# final
## final로 왜 사용하냐??
final로 선언 시 재정의 하는 것을 막을 수 있습니다.

만약 final로 선언된 메소드, 프로퍼티, 서브스크립트가 오버라이드를 하려고 하는 경우!!

오류가 발생하게 된다..

만약 
```swift
class Name {
    final var age = 18
}
```swift
class Kangho: Name {
    override var age: 19 {
        print("GangGang")
    }
}
```
이렇게 할 경우, 두번째 코드에서 age 부분을 오버라이드를 하려고 하기 때문에

오류가 발생하게 된다.