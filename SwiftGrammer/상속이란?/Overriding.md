# Overriding
### 오버라이딩이란?
서브 클래스는 슈퍼 클래스에서 상속할 인스턴스 메서드, 타입 메서드, 인스턴스 프로퍼티, 타입 프로퍼티, 서브스크립트를 구현할 수 있는데 이를 오버라이딩이라고 한다.

오버라이딩을 할 경우 앞에다가 override 키워드를 달아주지 않게 되면 오류가 터지게 된다.

override 키워드가 있을 경우 컴파일러는 슈퍼 클래스에 오버라이딩 선언한 것과 일치한 정의가 있는지 확인을 하고, 이것은 오버라이딩 정의가 올바른지 확인하는 것이다.

## 메서드 오버라이딩
상속받은 인스턴스 & 타입 메서드를 오버라이딩하여 하위 클래스 내에서 해당 메서드를 원하는대로 구현할 수 있다.

위 정의가 무슨 말이냐.

```swift
class Human {
    func expression() {
        print("I'm a human.")
    }
}

class KangHo: Human {

}
```
만약에 위와 같이 expression이란 메서드를 가지고 있는 Human 클래스랑 Human 클래스를 상속받는 KangHo이라는 클래스가 있다고 가정하자.

```swift
let WhoIsHe: KangHo = .init()
WhoIsHe.expression()
```
KangHo라는 클래스가 Human이라는 클래스를 상속 받기 때문에 Human이란 멤버들에 모두 접근할 수 있기에 위와 같이 적어도 오류가 터지지 않는 것이다.

실행하게 되면 
```
I'm a human.
```
Human에서 구현한 expression 메소드가 잘 실행될 것이다.

만약 KangHo라는 클래스에서 expression이란 메서드를 실행하게 되면 **나는 강호입니다.**를 출력하고 싶다면 어떻게 해야할까?

expression이라는 메서드를 KangHo 클래스 안에 직접 만들게 되면
```swift
class KangHo: Human {
    func expression() {
        print("나는 강호입니다.") //error!
    }
}
```
선언을 재정의 하려고 한다면 override 키워드를 사용한다면서 에러가 발생할 것이다.

상속받는 Human 클래스에 동일한 메서드를 두개를 선언 불가능하니 에러가 발생하는 것이다.

### 이를 해결하기 위해!!

오버라이딩을 사용하는 것이다.
```swift
class KangHo: Human {
    override func expression() {
        print("나는 강호입니다.")
    }
}
```
이렇게 KangHo라는 클래스는 Human이라는 슈퍼클래스의 expression 메서드를 오버라이딩 하는 것이다.

```swift
let WhoIsHe: KangHo = .init()
WhoIsHe.expression()
```

이렇게 KangHo라는 클래스를 인스턴스로 대고 실행하게 된다면

```
나는 강호입니다.
```

라고 잘 출력될 것이다.

만약 "나는 사람입니다." 와 "나는 강호입니다."를 둘 다 출력하고 싶다면?
```swift
class KangHo: Human {
    super.expression()
    override func expression() {
        print("나는 강호입니다.")
    }
}
```

위와 같이 super을 사용한다면 슈퍼 클래스에 접근해서 사용할 수 있다.
super를 사용하지 않으면 이미 KangHo클래스에서 expression 메서드를 재정의 했기 때문에 두 클래스에 있는 메서드들 전부 실행은 불가능 할 것이다.

출력하게 되면
```
나는 사람입니다.
나는 강호입니다.
```
라고 잘 출력될 것이다.

## 주의할 점
만약에 슈퍼 클래스에 정의 되어 있지 않는 메서드를 다른 메서드에서 상속 받아서 재정의 시킨다면?
```swift
class KangHo: Human {
    override func iDontKnow() { //error!!

    }
}
```

오버라이딩 하지 말라고 Xcode에서 에러 메세지를 뱉게 될 것이다.

그러니 주의하자!

## 프로퍼티 오버라이딩
프로퍼티 오버라이딩이란 상속받은 프로퍼티를 재정의하여 해당 속성에 대한 getter, setter를 제공하거나 상속받은 프로퍼티 값의 변경을 추적할 수 있도록 프로퍼티 옵저버를 추가할 수 있게 하는 것이다.

## 연산 속성 추가하기
서브 클래스에서는 상속된 프로퍼티의 특성이 저장인지 연산인지 알 수 없고 상속받은 프로퍼티의 이름과 타입 정도만 알고 있다.

오버라이딩을 할 경우 컴파일러는 슈퍼 클래스에 해당 이름과 타입을 가진 프로퍼티가 있는지 확인해야 되서 재정의 시 프로퍼티의 이름과 타입을 반드시 명시해야 한다.

#### 중요한 내용은!!

프로퍼티를 오버라이딩 할거라면 프로퍼티의 이름과 타입을 반드시 명시해야 한다는 것이다!

### 저장 프로퍼티
저장 프로퍼티에 저장 속성을 추가하는 오버라이딩은 될까?
```swift
class Human {
    var name = "KangHo"
}

class KangHo: Human {
    override var name: String = "KangHoo" //error!
}
```

안된다.

저장 프로퍼티의 name을 오버라이딩 할 수 없다고 에러가 발생할 것이다.

만약 저장프로퍼티 name에 연산속성인 get, set을 추가한 오버라이딩은 될까?

```swift
class KangHo: Human {
    var names = "KangHoo"

    override var name: String {
        return self.names
    }
}
```

저렇게 하면 안됩니다.

name이라는 프로퍼티를 getter만 가능하게 오버라이딩 시켜버리니 읽기, 쓰기 모두 가능한데 왜 서브 클래스가 읽기만 가능하게 하냐는 뉘앙스의 에러가 발생하게 된다.

#### 그러니!
저장 프로퍼티를 오버라이딩 하고 싶다면 
```swift
class KangHo: Human {
    var names = "KangHoo"

    override var name: String {
        get {            
            return self.names
        }

        set {
            self.names = newValue
        }
    }
}
```

위와 같이 get과 set을 모두 구현해주면 된다.

### 연산 프로퍼티 
연산 프로퍼티 같은 경우도 Human 클래스에 names라는 연산프로퍼티가 getter로만 구현되어 있다면 서브클래스에 get과 set을 모두 구현해주면 가능하지만

human 클래스에 names라는 연산프로퍼티가 getter/setter 둘 다 구현될 경우
서브 클래스에서 getter만 받을 경우 에러가 발생하게 된다.

## 프로퍼티 옵져버 추가하기
저장 프로퍼티의 경우, var로 선언된 프로퍼티만 오버라이딩으로 옵저버를 추가할 수 있다.

연산 프로퍼티의 경우, getter/setter 모두 구현된 경우만 오버라이딩을 옵저버를 추가 시킬 수 있다.

프로퍼티 옵저버는
- 저장 프로퍼팅에만 추가가 가능
- 연산 프로퍼티의 경우 서브 클래스에서 부모 클래스의 연산 프로퍼티를 오버라이딩 할 경우만 추가가 가능하다.

### 저장 프로퍼티
```swift
class Human {
    var name = "KangHo"
}

class KangHo: Human {
    override var name: String {
        willSet {
            print("name 값 변경 된다!\(newValue)")
        }
        didSet {
            print("name 값 변경 됨!\(oldValue)")
        }
    }
}
```

이렇게 슈퍼 클래스의 name이란 변수 저장 프로퍼티를, KangHo라는 서브 클래스에 재정의해서 프로퍼티 옵저버를 추가할 수 있다.

만약 타입을 명시해주지 않는다면 
```swift
class Human {
    var name = "KangHo"
}

class KangHo: Human {
    override var name { //error!

    }
}
```

타입을 명시하라는 에러가 발생하게 될 것이다.

## 연산 프로퍼티
연산 프로퍼티는 getter/setter가 모두 붙어있는 프로퍼티만 오버라이딩해서 프로퍼티 옵저버를 추가할 수 있고 그렇지 않을 경우 오류가 발생하게 된다.
___
이상으로 Overriding에 대한 공부를 마치도록 하겠다.