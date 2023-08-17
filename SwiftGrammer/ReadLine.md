# ReadLine of Swift
오늘은 ReadLine 이라는 것에 대해서 한번 배워볼 것이다.
## Readline이란?
표준 입력을 받아가지고 문자열로 반환시키는 것으로, 예시를 들어 내가 Int를 사용하든지 Double을 사용하든지 간에 어떠한 것이라도 모두 Strin인 문자열로 받아서 반환한다는 것이다.<br>
표준 입력은 지금 입력하는 라인의 끝이나 EOF에 닿을 때까지 한다.

> ## EOF란? <br>
> End Of File의 약자로, 입력하는 값들을 전부 반환해준다는 뜻이다.<br>
> ___

### 값을 입력하지 않는 경우
값을 입력해주지 않아서 발생하는 nil의 경우를 생각해서 이에 대해 unWrapping을 해주어야 하는데, 강제 unWrapping은 하지 말고 옵셔널 바인딩을 사용하자!!

예외도 있긴한데, 정말로 입력되는 값이 확실한다면야 !을 사용해도 된다.

### 단일 값이 아닌 배열이 입력될 경우

```swift
let array = readLine()!.split(separator: " ")
```

split을 사용해서 구분하여도 되고,

```swift
let array = readLine()!.components(separatedBy: " ")
```

components를 사용하는 것 또한 공백을 사용하여 값을 나눌 수 있다.

components 메서드는 

```swift
import Foundation
```

Foundation을 정의해야지만 사용이 가능하고, 리턴 값이 String이기에 바로 String으로 사용할 수 있다는 장점이 있지만... 

반면, 용량이 좀 늘어난다는 단점이 있다.

___
이상으로 ReadLine에 대한 공부를 마치도록 하겠다!!
