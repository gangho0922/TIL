# Timer

### 60초 타이머 예제
```swift
var timer : Timer?
var timerNum: Int = 0
```
먼저 타이머에 사용할 변수를 선언한 후 타이머에 사용할 값도 하나 선언해준다.

```swift
public func startTimer() {

}
```
타이머 시작을 알리는 함수도 하나 만들어주고 이 안에

```swift
if timer != nil && timer!.isValid {
    timer!.invalidate()
}
```
기존의 타이머가 이미 동작중이면 중지,

```swift
timerNum = 60

timer = Timer.scheduledTimer(timeInterval: 1, target: self, selector: #selector(timerCallback), userInfo: nil, repeats: true)
```
타이머 시작을 알리는 함수니까 타이머에 사용할 값을 초기화 시키고 1초마다 타이머가 시작하는 코드를 startTimer 함수안에다가 넣는다.

```swift
@objc func timerCallBack() {

}
```
타이머 시작을 알리기 위해서 타이머 동작 코드를 작성해주어야 하니

다음으로는 타이머 동작 코드를 작성해주고 이 안에 
```swift
self.timerButton.setTitle("\(timerNum)초", for: .normal)
```

이런식으로 초가 바뀔 때마다 타이틀을 변할 수 있도록 타이틀 설정을 해주고

```swift
if(timerNum > 45) {
        // 45초 초과일 때의 코드 작성
    } else if(timerNum > 30) {
        // 30초 초과일 때의 코드 작성
    } else if(timerNum > 15) {
        // 15초 초과일 때의 코드 작성
    } else {
        // 그 이하일 때 코드 작성
    }
```
같이 시간별 코드를 작성할 수 있도록 하고 (굳이 안해도 되긴함.)

```swift
if(timerNum == 0) {
    timer?.invalidate()
    timer = nil        
}
```
timer가 0일 시 종료 되는 코드를 넣어준다.

```swift
timerNum = timerNum - 1
```

타이머에 사용할 값을 감소 시키는 것도 잊지말기!!

___
이상으로 타이머를 만드는 것에 대한 공부를 마치도록 하겠다.