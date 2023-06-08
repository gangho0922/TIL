# computed property
### 먼저 stored property쪽을 보고 와주세요!

다음으로 설명할 것은 computed property,<br>
해석해보면 연산 프로퍼티인데요.
___
### 연산 프로퍼티(computed property)란?
저장 프로퍼티와 달리 저장 공간을 갖지 않고, 다른 **저장 프로퍼티**의 값을 읽어 연산을 실행하거나, 프로퍼티로 전달받은 값을 다른 프로퍼티에 저장하는 것을 말한다.

다른 프로퍼티에 저장되어야 하기 때문에 항상 var을 사용하여야 한다!

### 사용되는 부분
* 클래스
* 구조체
* 열거형

연산 프로퍼티의 생김새의 한 예시를 보여주자면
```swift
var bug: Type {
    get {
        butterfly
        return expr
    }
    set(bug) {
        butterfly
    }
}
```
여기 위와 같은데,<br>
위의 코드에서 get은 getter라고 부르고, set은 setter라고 부른다.

연산프로퍼티는 어떠한 값을 저장하는 것이 아니기 때문에 위의 예시 코드와 같이 타입 어노테이션을 통해서 자료형을 명시해야한다!!<br>
(선언된 자료 뒤에다가 {} 이걸 사용하는 것이 연산 프로퍼티를 사용하는 방법이다.)

내가 어떤 타입의 값을 받아서 다른 저장 프로퍼티에 저장하기 때문에 어떤 타입의 값을 리턴할 것인지도 명시해주어야 한다.
___
### getter?
뜻 그대로 얻는다는 뜻.<br>

따라서 어떤 저장 프로퍼티의 값을 연산해서 return할 것인지, return구문이 항상
존재해야한다!
___
### setter?
뜻 그대로 설정한다는 뜻.<br>

따라서 파라미터로 받은 값을 어떻게 설정할 것인지에 대해 구현한다.
___
이것에 대해 더 잘 이해하기 위해서 아래 코드를 한번 봐보자.
```swift
class Bug {
    var butterfly: String {
        get {
            return butterfly
        }
        set(name) {
            self.butterfly = name
        }
    }
}
```
위와 같이 타입 어노테이션 뒤에 {}가 시작되고 그 안에 get이랑 set이 있으면 butterfly는 연산 프로퍼티가 아닐까라는 생각이 들 수도 있는데

위 코드는....

### 틀렸다!!!

왜냐하면, 연산 프로퍼티는 다른 저장 프로퍼티를 가지고 하는 노는 녀석인데<br>
위에 적어져 있는 코드는 get과 set에서 butterfly라는 연산 프로퍼티를 가지고 놀고 있음..

실제 런을 해보면, getter가 무한대로 돌아가게 되는 무한 재귀 함수가 되게 된다..

따라서 연산프로퍼티를 사용하려면 다음과 같이
```swift 
class Bug {
    var name: String = "swallowtail butterfly"

    var butterfly: String {
        get {
            return name
        }
        set(name) {
            self.name = name
        }
    }
}
```
name 같은 읽거나 쓸 수 있는 저장 프로퍼티가 존재해야하고, 연산 프로퍼티에서 이런 다른 저장 프로퍼티를 읽거나 쓰는 작업을 해야한다.

name이란 저장 프로퍼티의 값을 읽어서 return하는 get,<br>
파라미터로 받은 값을 그대로 name이란 저장 프로퍼티에 저장시키는 set,<br>
위와 같이 구현해도 되지만 자신이 원한다면 다른 연산 작업을 직접 해줄 수 있다.

예시를 한번 봐보자!
```swift
class Bug {
    var name: String = "swallowtail butterfly"

    var butterfly: String {
        get {
            return self.name + "는 화려함"
        }
        set(name) {
            self.name = name + "는 내가 지어준 이름"
        }
    }
}
```
위와 같은 식으로 원하는 연산을 해서 getter를 작성해도 되고, 파라미터로 받은 값을 원하는 연산을 해서 setter를 작성할 수 있다.

그렇다면 이제 방금 만든 저 butterfly 함수는 어떻게 쓰는가???
___
### 연산 프로퍼티의 사용 방법
우리가 저장 프로퍼티를 사용했던 것처럼
```swift
let bigBug: Bug = .init()

print(bigBug.butterfly) //swallowtail butterfly는 화려함

bigBug.butterfly = "화려한나비"
print(bigBug.name)// 화려한나비는 내가 지어준 이름
```

이런식으로 저장 프로퍼티에 접근하는 것 마냥 접근해서 사용하면 된다.

연산 프로퍼티인 butterfly값을 읽으면 butterfly의 getter가 실행되어 "swallowtail butterfly" 라는 값이 나온 것이고,

연산 프로퍼티인 butterfly값을 쓰게 되면 "화려한나비"라는 값이 setter의 파라미터로 넘어가서 set함수가 실행되게 된다.
___
### newValue : set의 파라미터는 생략이 가능!!
```swift
set {
    self.name = newValue + "는 내가 지어준 이름"
}
```
이런식으로 파라미터를 생략하고 newValue로 대체할 수 있음!
___
### get-only
```swift
class Bug {
    var name: String = "swallowtail butterfly"

    var butterfly: String {
        return self.name + "는 화려함"
    }
}
```
이런식으로 set이 필요하지 않는다면 생략해서 쓸 수도 있지만
```swift
bigBug.butterfly = "화려한나비" //error!
```
get-only라 butterfly에 값을 할당할 수 없다는 에러가 발생하게 된다!!

___
### set-only
는 안됨 ㅎ

이상 computed property에 대한 공부를 마치도록 하겠다.