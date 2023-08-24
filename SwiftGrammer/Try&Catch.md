# Try Catch

오늘은 swift에서의 예외처리를 하는 방법에 대해서 한번 알아보자!!

# 1
```swift
enum energyError: Error {
    case unknown
    case energy(energyPercent: Int)
}

throw PhoneError.energy(energyPercent: 40)
```
먼저 case문을 사용해서 오류의 종류에 대해서 나눠 정의 시켜준다.

# 2
```swift
func electricEnergyStatus(energyPercent: Int) throws -> String {
    guard energyPercent != -1 else {
        throw energyError.unknown 
    }

    guard energyPercent > 40 else {
        throw energyError.energy(energyPercent: energyPercent)
    }

    return "enough Energy!!"
}
```
다음으로 throws 키워드를 사용해서 throwing 함수를 만들어서 오류를 처리하는 곳으로 전달하게 한다!

하지만 이렇게만 한다면 프로그램이 멈추게 된다...

그러니 다음으로 에러를 처리해주는 과정을 추가해주도록 하자!

# 3
처리하는데에는 3가지 방법이 있는데 
* do catch문
* try? 문
* try! 문

이렇게 있는데 하나하나 사용해보며 처리하는 부분을 작성해보도록 하자!

### do catch

```swift
do {
    try electricEnergyStatus(energyPercent: 40)
} catch energyError.unknown {
    print("It's a unknown error!!")
} catch energyError.energy() {
    print("low energyPercent...")
} catch {
    print("unexpected Error...")
}
```

### try? 문
```swift
let status = try? electricEnergyStatus(energyPercent: -1)
// 출력 시 nil 반환
```
```swift 
let status = try? electricEnergyStatus(energyPercent: 41)
// 출력 시 옵셔널로 감싸진 enough Energy!! 출력
```

### try! 문
```swift
let status = try! electricEnergyStatus(energyPercent: 41)
// 출력 시 enough Energy!! 출력
```
try! 문은 내가 정말 에러가 아니라고 판단할 시에 넣어준다. 넣어주면 옵셔널이 벗겨진다!

___ 
이상으로 Try Catch (예외처리) 부분에 대한 공부를 마치도록 하겠다!!