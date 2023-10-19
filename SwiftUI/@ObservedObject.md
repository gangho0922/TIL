# @ObservedObject
### @ObservedObject란?
observable 객체가 변경이 될 시 뷰에 업데이트를 시켜주는 기능을 한다.

### @ObservedObject 사용방법?
ObservableObject를 준수하는 인스턴스를 참조하기 위해 @ObservedObject를 선언해서 참조하여 사용한다.

### 주의할 점!!
ObservableObject는 class형태로만 사용가능하므로 struct형태로 사용하지 않을 것!!

### 사용 예시
```swift
import SwiftUI

class MyModel: ObservableObject {
    @Published var value = 0
}

struct ContentView: View {
    @ObservedObject var model = MyModel()

    var body: some View {
        Text("Value: \(model.value)")
        Button("Increment") {
            model.value += 1
        }
    }
}

```
이 같은 경우는 ContentView에서 @ObservedObject로 model을 선언하여 MyModel의 변화를 관찰하고, 버튼을 누를 때 value가 증가하면 뷰를 업데이트 시키는 작업을 합니다!

___
이상으로 @ObservedObject에 대한 공부를 마치도록 하겠습니다.