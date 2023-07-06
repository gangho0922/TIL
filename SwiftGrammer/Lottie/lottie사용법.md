# Lottie 사용하는 방법
내가 AI 축전이라는 걸 나가면서 자판기 키오스크와 연결하는 앱을 하나 만들려고 했었는데 그때 Lottie를 사용하라는 지시가 왔었다.

그래서 한번 그때 내가 알아보았던 Lottie에 대해 한번 정리해보자.
## Lottie란?
최소한의 코드로 벡터 기반 애니메이션이나 Art를 실시간으로 랜더링하는 모바일 라이브러리로, 애니메이션을 재생, 크기 조정, 루프 적용, 속도 향상, 속도 감소, 역회전 및 대화형 스크러빙을 하는 것이 가능하고, 애니메이션의 일부를 재생시키거나 반복 시킬 수 있다.
___
## Lottie 라이브러리
Lottie를 사용하기 위해서 라이브러리를 따와야하는데 나는 코코아팟과 카르타고, SPM중에 SPM을 사용해보겠다.

그러니 Lottie를 사용하기 위해서 먼저 Lottie 라이브러리를 다음 주소에서 가져오자!
```
https://github.com/airbnb/lottie-ios
```
이렇게 주소를 가지고 SPM으로 추가하게 되면
```swift
import Lottie
```
이런식으로 import해주게 되면 세팅 끝!
___
## Lottie를 사용해보기
먼저 Lottie에서 사용하는 확장 파일인 Json으로 하나 받아오자.

(아래 주소로 ㄱㄱ 뭐 다른 곳도 있겠지만..ㅎㅎ)
```
https://lottiefiles.com/featured
```
이 Json 파일을 Xcode에서 작업할 프로젝트에 넣어주자.
그렇게 되면 만일 json파일의 이름이 KangHo라면
```swift
let animationView: AnimationView = .init(name: "KangHo")
self.view.addSubview(animationView)
```
이런식으로 써서 사용할 수 있게 된다.

하지만!!

이렇게만 하게 되면 Lottie가 재생이 되지 않고 그냥 그림처럼 보여지게 된다.

이를 해결하기 위해서 몇가지 기능에 대해 살펴보자!
___
## 재생하기
```swift
사용할 로티.play()
```
이런식으로 play() 메서드를 사용하게 되면 Lottie를 재생할 수 있게 된다.
play() 메서드를 쓰게 되면 딱 한번만 애니메이션이 재생된 후 멈추게 된다.
___
## Loop 설정
```swift
사용할 로티.loopMode = .playOnce // 한번만 재생 뒤 종료
사용할 로티.loopMode = .repeat(3) // 3번 재생한 뒤 종료
사용할 로티.loopMode = .loop //무한으로 재생
사용할 로티.loopMode = .repeatBackwards(1) // 애니메이션을 실행한 후 실행한 애니메이션을 거꾸로 다시 실행
사용할 로티.loopMode = .autoReverse // 애니메이션을 실행한 후 실행한 애니메이션을 거꾸로 다시 실행, 무한 반복
```
이런식으로 사용하게 된다.
___
## 애니메이션 속도 조정
```swift
사용할 로티.animationSpeed = 3 // 애니메이션 3배속 재생
```
이런식으로 애니메이션 속도 조정도 가능하다.
## Frame을 아용해서 Animation재생
Frame을 사용해서 부분 재생을 할 수 있게 되는데 

### 여기서 Frame이란?
우리가 유튜브 같은 곳에서 영상을 볼 때 한장 한장의 그림으로 되어 있는 것인데, 여기서 한장 한장의 그림이 Frame이라고 한다.

```swift
사용할 로티.play(fromFrame: 10, toFrame: 30)
```
이런식으로 어디 Frame부터 어디 Frame까지 재생할 수 있게 하도록 할 수 있다.

### Tip
내 애니메이션의 Frame 갯수를 알고 싶다?
```swift
사용할 로티.animation?.endFrame
```
이런식으로 endFrame이라는 프로퍼티를 사용해서 알 수 있다.
___
## Progress 사용하기
Progress라는 것도 원하는 부분을 재생할 수 있도록 해주는 것이다.
```swift
사용할 로티.play(fromProgress: 0.4, toProgresss: 0.6)
```
이렇게 Progress를 이용해서 실행하게 되면, 이 말은 즉 40% ~ 60% 만큼 실행하겠다는 뜻으로 알면 좋을 것 같다.
___
## 원하는 Frame에서 멈추기
원하는 Frame에서 멈추게 하려면 
```swift
currentFrame
currentProgress
```
이런 프로퍼티들을 사용하게 되는데
```swift
사용할 로티.currentFrame = 40

혹은

사용할 로티.currentProgress = 0.6
```
이런식으로 사용해주게 되면 원하는 프레임에서 멈춰 보여주게 될 것이다.
___
이상으로 Lottie에 대한 공부를 마치도록 하겠다.
