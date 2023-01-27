# enum
#### enum : 열거형
## 1. 열거형이란?
  같은 주제로 연관된 데이터들을 멤버로 구성하여 나타내는 자료형

  ### EX)
  만약에 3가지 기준점으로 (top, mid, bottom)이 있다고 가정해보자!
```swift
var user1: String = "top"
var user2: String = "mid"
var user3: String = "midd"
var user4: String = "bottom"
```
근데 여기서 보면 user1과 user2는 둘다 같은  기준점인데 입력할 때마다 값을 직접 넣었다가는 저런식으로 오타가 나서 위에 "midd" 이런식으로 오타가 날 수 있음. (안정성과 가독성 👎)

<br>

### **따라서!!**
이처럼 공통된 주제에 대해서 이미 "정해놓은 값" 만 선택해서 받고 싶을 때 사용하는 것이 바로 열거형이다.<br>
열거형을 사용할 경우 코드 가독성도 좋아지고, 오타낼 일도 줄여주니 안정성도 향상된다!

## 2. 열거형 정의방법
<br>

### 2-1. 원시값이 없는 열거형
```swift
enum Position {
    case top
    case mid
    case bottom
}
```

이렇게 일일이 나열해서 적어도 되고!

```swift
enum Position {
    case top, mid, bottom
}
```
이렇게 쭉 나열해서 적어도 된다!

이렇게해서 작성한 것들을 바로
<br>
### **원시값이 없는 열거형** 이라고 부른다.

<br>

위에 선언한 열거형을 사용하려면
```swift
var user1 : Position = .top
```
이런식으로 선언한 case 앞에 점문법(.)을 사용하여 정의하여 접근한다!

### 2-2. 원시값이 있는 열거형
-Raw Value : case에 원시값을 지정 가능.

Raw Value에는 자료형이 3가지가 있음.

|1|2|3|
|:--:|:--:|:--:|
|NumberType|CharacterType|StringType|

- Number Type을 가지는 열거형
```swift
enum Position: Int {
    case top  //0
    case mid  //1
    case bottom  //2
}
```
이렇게 Int라는 타입을 enum으로 선언 시  이름 앞에 명시해주면, 가장 먼저 선언 된 case 부터 0부터 1씩 증가하는 값이 들어가게 된다.
<br>
만약에 내가 직접 값을 정해준다고 한다면?
```swift
enum Position: Int {
    case top  //0
    case mid = 10  //10
    case bottom  //11
}
```
Raw Value가 없는 case는, 바로 이전 case의 Raw Value에서 +1한 값으로 셋팅된다.
```swift
enum Position: Double {
    case top = 1.0
    case mid = 2.0 
    case bottom  
}
```
#### 만일 Int형이 아닌 자료형으로 했을 경우에, 모든 case에 대해 지정해주는 것이 아니면 **error**가 발생함!
그 이유는, 만약 다음 값이 없으면 이전 case에서 +1한 값을 가지게 되는데 이전 값이 정수값이 아닌 실수값이기 때문에 실수값에다가 정수값을 더해주는 꼴이 되므로 에러가 발생하는 된다.
- Character type을 가지는 열거형
```swift
enum Position: Character {
    case top = "t"
    case mid = "m"
    case bottom = "b"
}
```
주의할 점!

Character type으로 열거할 경우,
<br>**모든** case에 대한 Raw Value를 직접 선언해주어야 한다. (하나라도 없을 시 에러 발생.)
- String Type을 가지는 열거형
```swift
enum Position: String {
    case top //top
    case mid = "stom" //stom
    case bottom  //bottom
}
```
string은 character와 달리 Raw Value를 지정하는 않으면, case 이름과 동일한 Raw Value 값이 지정되게 됨.

### 원시값이 있는 열거형의 접근방법

rawValue라는 속성을 이용해 접근하면 된다.
<br>
Ex)
```swift
var user: Position = .top

user.rawValue
```

Raw Value를 통해서도 열거형을 생성할 수 있는데, 이땐 다음과 같이 생성자를 생성하도록 한다.
```swift
var user = PositionWithRawValue.init(rawValue: "top")
```
만약에 Raw Value 값이 없는 것을 대입할 때 반환되는 열거형은 옵셔널 타입임을 알아두도록 한다.
<br><br>
이상 enum에 대한 소개를 마치도록 하겠습니다.