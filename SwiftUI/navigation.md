# Navigation
### 스유에서의 Navigation이란?
스유에서의 navigation은 화면을 Push하거나 Pop 이동을 하기 위한 중요한 구성요소 중 하나다.

### 스유에서 navigation을 구현하려면?
* NavigationView
* NavigationLink

이것들로 구현할 수 있다!

## NavigationView
NavigationView를 사용하기 위해서는 다음과 같이 사용합니다.

```swift
struct ContentView: View {
    var body: some View {
        NavigationView {
            Text("Hello, World!")
        }
    }
}
```

만약 TabView내에서 사용하는 경우에는 NavigationView가 TabView내에 있어야 한다.

```swift
NavigationView {
    Text("Hello, World!")
        .navigationBarTitle("Navigation")
}
```
NavigationView내에서 navigationBarTitle()를 사용할 수 있다!
___
또한 displaymode로 커스터마이징을 할 수 있는데
```swift
.navigationBarTitle("Navigation", displayMode: .inline)
```
이런식으로 작성이 가능하다!!
## NavigationLink
```swift
NavigationLink(destination: Text("String"))
```
위와 같이 작성이 가능하고, 
SwiftUI의 NavigationView는 View의 맨 위에 NavigationBar를 표시하지만 다른 작업도 수행한다.

만약 Hello World를 클릭하면 새로운 탭으로 이동하는 코드를 작성한다면?

```swift
struct ContentView: View {
    var body: some View {
        NavigationView {
            VStack {
                NavigationLink(destination: Text("Detail View")) {
                    Text("Hello World")
                }
                
            }
            .navigationBarTitle("SwiftUI")
        }
    }
}
```

이런식으로 작성이 가능하다!
___
이상으로 navigation에 대한 공부를 마치도록 하겠다.