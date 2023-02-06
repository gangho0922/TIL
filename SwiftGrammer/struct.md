# struct
## 1. struct란?
struct는 클래스의 특별한 형태로, 데이터를 저장하기 위해 만들어지는 특별한 클래스이다. <br>
struct를 사용해서 여러 변수들을 결합해 하나의 타입을 만들 수 있다.
## 2. struct 기본 형태 만들기
struct는 다음 세가지 원칙을 이용해 만들어진다.
- struct에서 결합되는 변수들은 property라 부른다.
- struct 내부에 func을 넣을 수 있다.
- 생성자를 사용해 struct를 초기화 할 수 있으며 커스텀 생성자는 init()함수를 이용해 만들 수 있다.
<br><br>
위 세가지를 적용하면 Struct는 다음과 같이 만들어진다. 각 변수에 이름을 부여할 수 있어 가독성이 좋아진다.
```swift
struct StructName {
    let property1: Type1
    var property2: Type2

    init(_property1: Type1, _property2: Type2) {
        property1 = _property1
        property2 = _property2
    }
    func printProperty1(){
        print("property1 : \(property1)")
    }
}
```
다음과 같이 기본 값 설정도 가능!
```swift
struct StructName {
    let property1: Type1 = defaultValue
    var property2: Type2

    init(_property2: Type2) {
        property2 = _property2
    }

    func printProperty(){
        print("property1 : \(property1)")
    }
}
```
<br><br>

## 3. struct 예시
예를 사람으로 한번 들어보자!
<br>
사람은 이름, 나이, 체온을 나타낼 수 있는데 이를 이름, 나이 체온을 property로 사용하는 사람이라는 struct를 만들 수 있다.
<br>
추가적으로 struct에 사람이 아픈지 확인하는 func을 추가한다.
```swift
struct Person {
    let name: String
    let age: Int
    let temperature: Float

    init(_name: String, _age: Int, _temperature: Float) {
        name = _name
        age = _age
        temperature = _temperature
    }
    func isSeek() -> Bool {
        return temperature > 37.5
    }
}
```
이렇게 코드를 작성하면 사람 객체는 다음과 같이 만들 수 있다!
```swift
let person = Person(_name: "Kangho",_age: 18,_temperature: 38.5)
```
자 이제 방금 짠 코드를 합쳐 만든 사람 객체를 가지고 사람이 아픈지 확인해보자!
```swift
struct Person {
    let name: String
    let age: Int
    let temperature: Float

    init(_name: String, _age: Int, _temperature: Float) {
        name = _name
        age = _age
        temperature = _temperature
    }
    func isSeek() -> Bool {
        return temperature > 37.5
    }
    let person = Person(_name: "Kangho",_age: 18,_temperature: 38.5)

    print("Is Person seek? \(person.isSeek())")
}
```
```
Is Person seek? true
```
사람의 체온이 38.5도로 37.5도를 넘기 때문에 아픈 것으로 판단 돼 true가 출력되는 것을 볼 수 있다!

<br><br><br>
<hr>
이상으로 struct에 대한 소개를 마치도록 하겠다.