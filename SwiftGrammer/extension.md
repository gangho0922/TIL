# extension
## 1. 확장(extension)이란?
기존 클래스, 구조체, 열거형 타입에 새로운 Property, Method, Initializer 등을 추가하는 것으로,
원본 타입(소스 코드)에 접근하지 못하는 타입들도 확장해서 사용할 수 있다. <br><br>
extension이란 키워드를 사용하여 확장한다
### Ex)
```swift
extension SomeType: SomeProtocol,AnotherProtocol {
}
```
이렇게 확장을 사용한 뒤에다가 타입을 쓰는 것이다!
```swift
let point: CGPoint = .init(x: 10, y: 20)
```
다음은 CGPoint라는 구조체가 있는데 이것은 코어 그래픽에 포함되어 있는 구조체이다.
<br>
```
x : 10, x : 20
```
만약에 내가 point를 다음과 같이 이쁘게 출력하고 싶다면?
```swift
print("x: \(point.x), y: \(point.y)")
```
이렇게! 원본 코드는 그대로 두고, 말 그대로 내가 원하는 기능만 해당 타입에 확장하는 것이다.
```swift
extension CGPoiont {
    func printPoint() {
        print("x: \(self.x), y: \(self.y)")
    }
}
```
이렇게! 확장자를 쓰고 다음에 이름을 쓰는 것이다.
그리고 그 안에 내가 원하는 메서드로 printpoint라는 메서드를 구현한다면?
```swift
point.printpoint()
```
마치 원래 CGPoint 함수에 printPoint 함수가 있었던 것처럼 사용할 수 있다.
## 2. 확장에 프로퍼티 추가
⭐️ 확장에는 저장 프로퍼티를 추가할 수 없으며, 오로지 **연산 프로퍼티** 만 추가 가능하다.
<br>
만약에 추가할려고 한다면?
```swift
extension Int {
    var zero: Int = 0 // error
}
```
확장에 저장 프로퍼티가 포함되면 안된다는 에러가 발생할 것이다.<br>
따라서 다음과 같이,
```swift
extension Int {
    var half: Int {
        return self / 2
    }
}
``` 
이렇게 선언된 연산 프로퍼티는
```swift
let num = 100
print(num.self)
```
이렇게 모든 Int형 타입에서 사용이 가능하다.
## 3. 확장에 메서드 추가
```swift
//타입 메서드
extension  Int {
    static func printZero() {
        print(0)
    }
}
Int.printZero() // 0
```
```swift
//인스턴스 메서드
extension Int {
    func printDouble() {
        print(self * 2)
    }
}
let num = 100
num.printDouble() // 200
```
예제만 보고 빠르게 패스~
## 4. 확장에 생성자(initializer) 추가
⭐️ 기존 타입에 새로운 이니셜 라이져를 추가할 수 있다.
### 4-1. Class에서의 생성자 추가
Designated initializer는 추가 (x) <br>
Convenience initializer는 추가 (o) <br>
deinitializer는 추가 (x) <br>
<br><br>
여기서!
<br>
Designated Initializer : 클래스의 모든 속성(슈퍼 포함)을 초기화 하는 생성자.
<br>
Convenience Initializer : 유틸리티 성격의 생성자.
<br><br>
이둘의 자세한 설명은 생성자 부분에서 다루겠다.
```swift
extension NSString {
    deinit{ print("deinit") }
    //error
}
```
다음과 같이, Deinitializer(소멸자)는 extension으론 구현이 불가.(원본 클래스에서만 구현해야 한다.)
```swift
extension NSString {
    init() {} //error
}
```
Designated initializer로도 구현 불가.
```swift
extension NSString {
    convenience init(name: NSString) {
        self.init()
    }
}
```
이렇게 convenience initializer만 되게 되는데, convenience initializer는 최종적으로 Designated initializer를 호출해야 된다.
### 4-2. Struct에서 생성자 추가
⭐️ extension으로 생성자를 추가할 경우, Memberwise initializer를 보존하며 새로운 생성자를 추가할 수 있다.
<br><br>
구조체는  클래스와 달리,<br> "**기본 생성자(memberwise Initializer)**"를<br> 자동으로 제공한다.
<br><br>
더불어 구조체건 클래스건 인스턴스 생성자 호출이 끝나는 시점엔 모든 프로퍼티가 초기화 되어 있어야한다.
때문에 프로퍼티는 기본값을 지니지 않을 경우, 무조건 생성자에서 초기화해야 했다.
근데? <br>다음 예제를 한번 봐보자.
```swift
struct PointStruct {
    let x: Int
    let y: Int
}

class PointClass {
    let x: Int
    let y: Int // error!!
}
```
구조체는 init함수가 없이도 error가 뜨지 않는데, 클래스만 init함수가 없다고 에러가 발생한다.
<br>
그이유는 클래스와 달리 구조체가 모든 프로퍼티를 초기화 할 수 있게 하는 Memberwise라는 생성자를 "따로 생성자를 구현하지 않았을 경우"에 한에서 자동을 제공하기 때문이다.
<br><br>
위처럼 PointStruct는 생성자를 따로 구현하지 않았기 때문에, 자동으로 Memberwise Initializer가 제공된다.

![member initializer](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqeaWP%2FbtqZP1ZGsn1%2FF4dYrxwQD0TSBGlXf2uLlK%2Fimg.png)
이게 Memberwise initializer이다.
<br>
만약 내가 생성자를 **직접!** 구현한다면
```swift
struct PointStruct {
    let x: Int
    let y: Int
 
    init(value: Int) {
        self.x = value
        self.y = value
    }
}
```
이렇게 직접 구현해버리면
![no serve](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5XWYY%2FbtqZP2RRJVI%2F04DpYuJteJiH1KAm7NpM7K%2Fimg.png)
Memberwize initializer는 더 이상 제공하지 않는다.
그런데?
```swift
struct PointStruct {
    let x: Int
    let y: Int
}

extension PointStruct {
    init(value: Int){
        self.x = value
        self.y = value
    }
}
```
extension을 통해 구조체 한정의 생성자를 추가한다면?
![conserve](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPkNye%2FbtqZMmXQrqw%2F2iH6IuTjGjS7U9ZfG4q2r0%2Fimg.png)
Memberwise initializer를 보존하며 생성자를 추가할 수 있다!!

## 5. 확장에 Subscript 추가
```swift
extension String {
    subscript(idx: Int) -> String? {
        guard (0..<count).contains(idx) else {
            return nil
        }
        let target = index(startIndex. offsetBy: idx)
        return String(self[target])
    }
}
```
위와 같이, extension을 통해 subscript를 직접 구현해주게 되면,
```swift
let swift = "Hello, swift!!"
swift[0] //optional("H")
swift[100] // nil
```
이렇게 []를 통해서 내가 원하는 인덱스의 문자를 접근할 수 있다!!
## 6. 확장에 중첩 타입 추가
```swift
 extension Int {
    enum Kind {
        case negative
        case zero
        case positive
    }
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
 }
 ```
 이렇게 Int 타입의 extension 안에 Kind라는 enum을 중첩해서 선언할 수 있고,
 ```swift
 let num = 100
 print(num.kind) // positive
 let minum = -100
 print(minum.kind) // negative
 ```
 이런식으로 사용도 가능하다.
 ## 7. 확장에 프로토콜 추가
 ```swift
 struct Human {
    let name: String
 }
 let swift: Human = .init(name: "swift")
 let swiftswift = swift
 swift == swiftswift //error!!
 ```
 내가 선언한 Human이라는 인스턴스끼리 == 연산자를 이용해서 비교하고 싶은데 에러가 뜨면서 비교할 수 없다고 한다!
 <br>
 왜냐하면 == 연산자를 사용하고 싶다면 Equatable이란 프로토콜을 채택하고 있어야하기 때문이다!!
 ```swift
 struct Human: Equatable {
    let name: String 
    public static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.name == rhs.name
    }
 }
 ```
 다음과 같이 구조체 자체에 프로토콜을 추가해도 되지만, 보통 프로토콜을 채택할 땐, **원본은 원본에 관련한 함수들만 두고**!!
 ```swift
 struct Human {
    let name: String
 }
 extension Human: Equatable {
    public static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.name == rhs.name
    }
 }
 ```
 extension을 이용하여, 해당 프로토콜에 맞는 메서드만 구현하는 것이 유지보수 및 가독성 면에서 좋다.
 ### 7-1. extension을 통해 코드 가독성 높이기
 만약 하나의 ViewController에서 TableViewDataSource & CollectionViewDataSource를 채택해야 된다면,
 ```swift
 class ViewController: UIViewController, UITableViewDataSource, UICollectionViewDataSource {
 
    override func viewDidLoad() {
    }
 
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    }
 
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    }
 
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
    }
 
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
    }
}
```
다음과 같이 원본 클래스에 모든 것을 작성해도 되지만, 상당히 지저분해 보인다는 것을 느낄 수 있을 것이다.<br>
그렇다면 우리 한번 extension을 사용하여 한번 다시 짜보자!
```swift
class ViewController: UIViewController {
    override func viewDidLoad() {
    }
}
 
extension ViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    }
 
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    }
}
 
extension ViewController: UICollectionViewDataSource {
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
    }
 
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
    }
}
```
이렇게 extension을 통해 프로토콜 기능별로 분리한다면 코드가 더 깔끔해진다!
<br>
또한 extension은 Objective-C의 #pragma mark 기능도 하기 때문에
<br>
**extension에 따라 트리의 구조가 바뀐다!!**
따라서 잘 활용하면 좋은 코드를 짤 수 있다.

## 8. 범용타입에서 where을 통해 확장에 조건 두기
이 부분은 Generic이란 키워드를 공부하고 다시 설명하도록 하겠다. 자세한 부분은 [여기!](https://babbab2.tistory.com/124) 를 클릭해서 제일 아래부분을 봐주길 바란다.
<br><br>
이상으로 extension에 대한 소개를 마치도록 하겠다.