# Codable
Codable이란?
자기 자신을 변환하거나 외부 표현으로 변할 수 있는 타입이다.

Codable이 프로토콜들로 이루어진 Alias이다.

```swift
typealias Codable = Decodable & Encodable
```

Codable은 Decodable과 Encodable을 동시에 준수하는 타입이다.

### 여기서!!

#### Encodable이란?
외부표현으로 변환할 수 있는 타입이다.

여기서 말하는 외부표현이란 우리가 흔히 아는 JOSn과 같은 것들이 있는 것으로 보면 되겠다.

#### Decodable이란?
자신으로 변환할 수 있는 타입이다.

___
### Codable 사용 방법
예제를 통해서 한번 알아보자!!

Encoding과 Decoding이 모두 필요한 경우에는 모두 채택해도 된다.

만약에 아래와 같은 구조체가 있다고 한다.
```swift
struct Person {
    var name: String
    var age: Int
}
```
Codable type을 만들기 가장 쉬운 방법은 이미 Codable을 만족하는 타입으로 프로퍼티를 선언하는 것이다.

저 위의 코드에다가 Codable을 채택한다치면
```swift
struct Person: Codable {
    var name: String
    var age: Int
}
```
이런식으로 될 것이다. 이제 이 구조체는 Encodable과 Decodable을 동시에 채택한 형태가 된 것으로 이 구조체를 채택한 인스턴스는 자기자신을 변환하거나 외부 표현으로 변할 수 있는 타입이 된 것이다.

자세한 내용은 공식 문서를 참조바란다.

### Encoding
Encoding의 예제를 한번 봐보자!
```swift
let encoder = JSONEncoder()

let information = Person(name: "강호", age: 18)

let jsonData = try? encoder.encode(information)

if let jsonData = jsonData, let jsonString = String(data: jsonData, encoding: .utf8) {
    print(jsonString)
}
// Data형시의 jsonData를 String으로 변환시킴.
```
출력시키면 
```swift
{"name":"강호","age":18}
```

이렇게 출력된다.
```swift
encoder.outputFormatting = .prettyPrinted
```
이렇게 추가해주면 좀 더 보기 좋게 출력되게 된다.

### Decoding
Decoding하는 방법은 Encoding을 했던 것과 비슷하게 Encoding했던 자리에 Decoding을 해주면 된다.

```swift
let decoder = JSONDecoder()

var data = jsonString?.data(using: .utf8)

if let data = data, let information = try? decoder.decode(Person.self, from: data) {
    print(information.name)
}
```
위와 같이 Encodable 했던 걸 Decodable로 바뀌주기만 하면 된다.
___
이상으로 Codable에 대한 공부를 마치도록 하겠다.