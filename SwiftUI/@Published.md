# @Published
### @Published란?
SwiftUI에서 'ObservableObject' 프로토콜을 준수하는 클래스의 속성을 선언할 때 사용한다. 이 속성의 변경사항을 관찰 가능하도록 만들어서 뷰가 이 속성에 반응할 수 있도록 한다.

### 주요포인트?
#### 1. ObservedObject Protocol
@Published 속성 래퍼를 사용하려면 해당 클래스가 ObservedObject Protocol을 준수해야한다.

#### 2. 속성 선언
@Published 속성 래퍼를 사용하여 속성을 선언할 때 해당 속성을 @Published로 표시해야한다!

#### 3. 자동 업데이트
@Published 속성이 변경될 때에는 스유가 뷰를 업데이트한다! 이것으로 데이터 모델의 변경 사항이 뷰에 자동으로 반영되도록 해준다!

### 사용예시
```swift
import SwiftUI

class MyModel: ObservableObject {
    @Published var value = 0
}
```
위는 MyModel이 ObservedObject 프로토콜을 준수하고, value 속성은 @Published로 표현되어 있는 코드이다.

@Published를 이용해서 value가 변경될 때마다 뷰가 자동으로 업데이트 되도록 하였다.

### 마무리

@Published 속성 래퍼는 스유에서 양방향 바인딩을 구현할 때 유용하며, 뷰와 데이터간의 통신을 효율적이게 해준다!

___ 
이상으로 @Published에 대한 공부를 마치도록 하겠다.