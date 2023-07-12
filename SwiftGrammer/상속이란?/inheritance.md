# inheritance - 상속
## 상속이란?
클래스만 상속이 가능하며 상속은 다중 상속이 아닌 단일 상속만 허용한다. 클래스는 메서드, 프로퍼티 및 기타 특징들을 상속할 수 있다.

### 기본 클래스
아무 클래스도 상속 받지 않는 클래스를 기본 클래스라고 한다.
```swift
class Dog {
    var name: String?
    var age: Int?
}
```
위의 클래스는 Dog라는 class의 이름 뒤에 아무런 클래스 링크가 오지 않았기 때문에 아무런 클래스도 상속 받지 않는 기본 클래스임을 알 수 있다.

```swift
class Dog: Hashable {
    var name: String?
    var age: Int?
}
```
위의 같은 경우는 뒤에 class가 아닌 프로토콜이 붙었기 때문에 기본 클래스라고 할 수 있다.

이름 뒤에 클래스가 아니여야 기본 클래스라고 할 수 있다.

## 서브 클래싱
기본 클래스를 기반을 새로운 클래스를 만드는 작업으로, 서브 클래스 이름 옆에 :을 쓰고 먼저 상속 받고자 하는 슈퍼 클래스의 이름을 쓴다.

만약에 MyPet 이라는 클래스를 만들고 이 클래스가 Dog라는 클래스의 name, age 프로퍼티를 모두 가지고 필요한 멤버를 더 추가한다면
```swift
class MyPet: Dog {
    var hobby: String?
}
```

이런식으로 작성하여 MyPet이라는 class를 선언 시 :를 사용해서 가장 먼저 상속받을 클래스를 선언해주면 된다.

상속받는 Dog클래스의 프로퍼티인 name, age 그리고 새로 추가해 자신이 가지고 있는 hobby 까지 모두 접근할 수 있다.

```swift
let kkommi: MyPet = .init()
kkommi.age
kkommi.hobby
```

이렇게!!

가능하다.

여기서 상속 받고자 하는 Dog 클래스를  **슈퍼 클래스**, Dog 클래스를 상속 받는 MyPet 클래스를 **서브 클래스** 라고 한다.

## final은 상속 금지!
```swift
final class Dog {
    var name: String?
    var age: Int?
}
```
이런식으로 하면 아무도 Dog 클래스를 상속 받을 수 없게 된다.
___
이상으로 상속에 대한 공부를 마치도록 하겠다.