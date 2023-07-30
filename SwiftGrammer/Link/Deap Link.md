# Deap Link
이번 2023년도 kwdc 행사에 다녀오면서 Zeon님께서 Link에 대해 공부하라고 하시길래 이렇게 Link에서 Deap Link를 먼저 공부해보기로 했다.
### 딥링크란?
서버에서 앱에 URL을 전송하면 앱에서 그 URL을 가지고 파싱해서 특정 화면으로 전환하는 개념이라고 생각하면 되겠다.

iOS에서 Deap Link를 구현하는 방법에는
* URL Scheme
* Universal Links

이것들이 있는데 Universal Links가 Scheme 보다 먼저 나와서 Universal Links가 더 많이 사용되지 않을까 싶기도 하는데 Scheme 방식도 안쓰지는 않는 것 같다.

## 구현 방법
### URL Scheme
URL Scheme 방식은 어떤 scheme을 사용할 건지만 앱에서 설정해주면 된다.

URL 컨벤션은 앱 이름으로 시작해 path, query 부분으로 웹 URL처럼 설정하는게 보통이다.

URL Scheme 방식으로 딥링크를 사용하려면 프로젝트의 Info에서 URL Type에서 scheme을 먼저 등록해줘야 한다. 그런 다음에 **scheme://resource** 이런식으로 URL 포맷을 맞춰주어야 한다.

사파리나 WKWebView에서 링크를 클릭하면 AppDelegate만 있을 때 **application(app: url: options: )** 이게 아니면 SceneDelegate에서 **scene(scene: URLContexts: )** 를 호출하게 된다.

링크를 클릭했을 때, 앱스토어가 설치되어 있는지 확인 후에 설치되어 있으면 앱으로 이동하고, 그렇지 않으면 앱스토어로 이동한다.<br>
URL Scheme 문자열을 통해서 URL 인스터를 생성한 후 **UIApplication.canOpenURL(_: )** 로 URL Scheme의 유효성을 확인한 뒤에 open을 호출시킨다.

프로젝트에 따라서 딥링크를 처리하는게 각각 다른 것 같다.
___
### Universal Links
유니버셜 링크는 웹사이트나 앱 콘텐츠로 부드럽게 링크를 걸어준다. 앱이 설치되어 있지 않더라도 사용자에게 통합된 모바일 경험을 줄 수 있다는 그런 장점이 있다고 소개하고 있다. iOS 9 이상에서 지원되어서 현재 거의 모든 앱에서 유니버셜 링크를 사용할 수 있는 것으로 본다.

유니버셜 링크 같은 경우에는 **Signing & Capabilities**로 들어가서 **Associated Domains**에다가 Domain을 등록시켜준다.

```
applinks:my_app.page.link
```
위와 같은 식으로 등록이 된다.

링크를 클릭했을 때 링크가 설치되어 있다면 묻지 않고 바로 앱으로 연결되고 아니라면 앱스토어에 연결되게 된다. 

외부에서 딥링크를 탭하면 AppDelegate의 **application(_: open: options: )** 를 통해서 앱을 시작시킨다.

SceneDelegate가 있는 프로젝트에서는 SceneDelegate의 **scene(scene: userActivity: )** , **scene(scene: URLContexts: )** 에서 핸들링 하게 된다.
```swift
func scene(_ scene: UIScene, continue userActivity: NSUserActivity)

func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>)
```

## 둘의 장점과 단점
### URL Scheme
#### 장점
구현이 쉽고, 백엔드가 필요하지 않다.
#### 단점
항상 허용 여부를 묻는 팝업을 띄우고 안드로이드 등 다른 플랫폼에서는 동작하지 않는다. 그리고 앱이 설치되어 있지 않다면 동작하지 않는다.
### Universal Links
#### 장점
허용 여부를 묻지 않고 브라우저를 열지 않고 다른 플랫폼과도 호환이 가능하다. 앱이 설치되지 않은 경우에는 fallback URL을 사용한다.
#### 단점
SSL 있는 백엔드 필요하다.

AASA파일을 well-known이나 root 디렉터리에 추가해야 한다.

그리고 구현이 더 복잡하다.
___
한마디로 URL Sceme의 장점과 단점이이 Universal Links의 단점과 장점으로 되는 것이다.

___ 
이상으로 Deap Link에 대한 공부를 마치도록 하겠다.