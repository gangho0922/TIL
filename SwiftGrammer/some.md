# some
## some이란?
Swift 5.1에 나왔던 새로운 기능으로 computed property인 body안에 불투명한 타입이 존재한다는 것을 뜻한다.
___
### 여기서!
## 불투명한 타입이란?
```swift
protocol Shape {
    func describe() -> String
}

struct Square: Shape {
    func describe() -> String {
        return "square eyes"
    }
}

struct Ractangle: Shape {
    func describe() -> String {
        return "ractangle eyes"
    }
}
```
위와 같은 코드가 있을 때 
```swift
func makeShape() -> Shape {
    return Square()
}
```
makeShape는 불투명한 타입으로 불투명한 타입을 return 하면 swift에서 오류를 발생 시킬 것이다.

이렇게 불투명한 타입을 적은 부분에서 에러가 발생하지 않게 하려면
```swift
func makeShape() -> some Shape {
    return Square()
}
```
이런식으로 위에서 설명했던 코드에다가 some만 넣어주면 해결이 가능하다.
타입을 미리 지정시켜주는 generic 타입과는 달리 함수 내부의 코드에 따라서 구체적인 리턴 타입이 달라지게 된다.
___
## 사용 예시
이 some은
```swift
struct MyFirstView: View {
    var body: some View {
        Text("Hello World")
    }
}
```
위의 코드처럼 swiftUI에서 자주 쓰인다.
___
## 이걸 도대체 왜 써야할까?
예시를 한번 봐보자.
```swift
func test() -> Array<Int> {
    return [1, 2, 3]
}
```
위와 같이 배열의 1, 2, 3을 리턴 시키는 기능을 만들어달래서 만들었는데 
갑자기 상사가 딕셔너리로 바꿔오라고 시키면 아무래도 코드수정도 해야되는 상황이 오니 매우 귀찮아지게 된다. (예를 들어서 ㅎ) 

이럴때를 위해서 some을 써주면 되는 것이다!

```swift
func test() -> some Collection {
    return [1, 2, 3] // 상사 닥달 전
}
```
```swift
func test() -> some Collection {
    return ["A": 1, "B": 2, "C": 3] //상사 닥달 후
}
```
위의 코드들과 같이 some을 사용하게 되면 내부 구현만 수정하고 다른 코드들을 수정할 필요가 전혀 없어진다!

___
지금까지 some에 대한 공부를 마치겠다.
