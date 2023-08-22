# UUID
### UUID란?
UUID는 Universally Unique Identifier의 약자로, UUID 표준에 따라 이름을 부여할 시 고유성이 완벽히 보장되진 않지만, 실제로 사용한다고 할 때 중복될 가능성이 거의 없다고 하기 때문에 널리 사용된다고들 한다.

### UUID 형식
UUID는 32개의 숫자 및 알파벳과 4개의 하이픈으로, 총 36개의 문자열로 이루어져 있다!!

예)
```
C39E3827-A73C-BA32-5E3E-E8C7A65E376C
```

### 사용 가능한 UUID 갯수??
총 사용 가능한 UUID 갯수는....

#### 무려...!!
약 10의 38승개라고 한다...ㄷㄷ

### UUID가 식별 가능한 것

UUID는 Types와 interfaces 그리고 other items를 식별할 수 있다고 한다.
___
### UUID 생성
C언어 구조로부터 생성
```swift
init(uuid: uuid_t)
```
문자열 표현으로부터 생성
```swift
init?(uuidString: String)
```
특정 Decoder로부터 Decode해서 생성
```swift
init(from: Decoder)
```
___
### UUID 가져오기
UUID를 byte로 반환
```swift
var uuid: (UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8, UInt8)```
UUID로부터 생긴 문자열 반환
```swift
var uuidString: String
```
___
### UUID 비교 방법
두개의 값이 같은지 아닌지를 나타내는 Bool 값을 반환한다.
```swift
static func != (UUID, UUID) -> Bool
```
두개의 값이 같은지를 나타낸다.
```swift
static func == (UUID, UUID) -> Bool
```
___
### UUID를 Encoding
UUID를 특정 Encoder에 encode ㄱㄱ
```swift
func encode(to: Encoder)
```
___
### UUID를 나타내는 방법
```swift
var description: String // UUID에 대한 텍스트 설명
```
```swift
var debugDescription: String // 디버깅에 적합한 UUID에 대한 텍스트 설명
```
```swift
var customMirror: Mirror // UUID를 반영하는 Mirror
```
```swift
var hashValue: Int // UUID의 계산된 hash 값
```
```swift
func hash(into: inout Hasher) // 값의 필수 구성 요소를 특정 해시에 공급하여 해시
```

### UUID의 특징

* 앱을 재실행해도 값은 저장된다.
* 앱의 공급 업체가 같을 시 UUID 값도 같다.
* 앱을 삭제했어도 공급 업체가 제공하는 다른 앱이 남아있다면 UUID 값은 유지된다.
* 공급 업체를 전부 다 삭제한다면 UUID값은 유지가 안된다.

___
이상으로 UUID에 대한 공부를 마치도록 하겠다.