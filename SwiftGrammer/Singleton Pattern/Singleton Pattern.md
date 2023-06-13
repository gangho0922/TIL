# Singleton Pattern
## 싱글톤 패턴(Singleton Pattern)이란?
특정 용도로 객체를 하나만 생성해서, 공용으로 사용하고 싶을 때 사용하는 디자인 유형을 뜻한다!!
___
만약에 내가 다음과 같이 사용자의 정보를 저장하는 클래스를 만들었다고 하자.
```swift
class User {
    var name: String?
    var address: String?
    var nickname: String?
}
```
그리고 a ViewController에서는 name
```swift
//a ViewController
let user = User()
user.name = "kangho"
```
b ViewController에서는 address
```swift
//b ViewController
let user = User()
user.address = "대한민국"
```
c ViewController에서는 nickname을 입력받아서
이것을 User 클래스에다가 다음과 같이 저장한다고 치자.
```swift
//c ViewController
let user = User()
user.nickname = "kangho5555"
```
이런식으로 a,b,c ViewController에서 각각 User 객체에 값을 저장했다면,
![](Signleton%20Pattern1.png)

이런식으로 각 인스턴스의 프로퍼티에만 저장 될 것이고, 이게 아닌 우리가 원하는건 한 instance에 모든 정보가 들어가는 것이다.

이를 해결하기 위해서 인스턴스는 참조타입이라, User 인스턴스를 한번 생성해서 이 인스턴스를 A-> B -> C 이런식으로 참조가 필요할 때마다 넘겨주면 되긴한다.

하지만!!!

그렇게 되면 코드가 지저분해질 것이다.

그래서, 이 클래스에 대한 인스턴스는 최초 생성될 때 딱 한번만 생성해서 전역에다가 두고, 그 이후로는 이 인스턴스만 접근만 하자는 해결 방법이 바로~~~

### Singleton Pattern이다!!

싱글톤을 사용하는 다음 그림처럼 그려지게 된다.
![](Singleton%20Pattern2.png)

이런식으로 한 인스턴스에다가 어디 클래스에서든 접근 할 수 있도록 하는 것이 싱글톤이다.
___
## Singleton을 만드는 방법
Objective-C 와는 달리 Swift는 간단하다.

### static 프로퍼티로 인스턴스 생성하기
```swift
class User {
    static let shared = User()

    var name: String?
    var address: String?
    var nickname: String?
}
```
전역에 저장되어야하니 인스턴스를 저장할 shared라는 저장 프로퍼티를 하나 생성해준다.
### init 함수 접근제어자를 private로 지정시키기
```swift
class User {
    static let shared = User()

    var name: String?
    var address: String?
    var nickname: String?

    private init() {}
}
```
init을 호출 시켜서 인스턴스를 다시 생성하는 것을 막기 위해서 init() 함수 접근제어자를 private으로 지정해주자.

이러면 싱글톤 만들기, 어렵지 않쥬~?
___
### Singleton Class 접근 방법
아까 생성해뒀던 static 프로퍼티를 이용해서 다음과 같이 접근하면 된다.
```swift
//a ViewController
let user = User.shared
user.name = "kangho"
```
```swift
//b ViewController
let user = User.shared
user.address = "대한민국"
```
```swift
//c ViewController
let user = User.shared
user.nickname = "kangho5555"
```
어느 클래스에서든지 간에 shared라는 저장 프로퍼티로 접근하면 하나의 인스턴스를 공유하는 것이 된다.
___
## Singleton의 장단점

장점
> * 한번의 인스턴스만 생성하므로 메모리 낭비를 방지 가능.
> * 싱글톤 인스턴스는 전역 인스턴스로 다른 클래스들과 자원 공유하기가 쉬움.
> * DBCP(DataBase Connection Pool)처럼 공동된 객체를 여러개 생성해서 사용해야되는 상황이 온다면 많이 사용.(쓰레드풀, 캐시, 대화상자, 사용자 설정..등등)

단점
> * 싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시켰을 경우 다른 클래스의 인스턴스들 간 결합도가 높아져서 "개방=폐쇄" 원칙인 객체 지향 설계 원칙에 어긋나서 수정과 테스트가 어려워짐.

___
## 참고자료 ~
참고자료 [gogo](jeong-pro.tistory.com/86)
___
이상 싱글톤 패턴에 대한 공부를 마치도록 하겠다.