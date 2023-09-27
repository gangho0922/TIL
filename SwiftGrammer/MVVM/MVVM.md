# MVVM

### MVVM이란?
Model - View - Controller로 이루어져 있는 MVC 패턴과 달리,<br>
Model - View - ViewModel로 이루어져 있는 패턴으로

### 한마디로 말하자면?
Model의 데이터를 VIewModel이 가공시켜서 그렇게 해서 가공시킨 ViewModel을 보여주는 View로 이루어진 패턴이라고 할 수 있다.

#### 여기서!
### Model?
내가 다루게 될 데이터를 의미한다.
### View?
UIVIew들의 서브 클래스를 의미한다.
### ViewModel?
내가 곧 다루게 될 데이터인 Model을 View에 보일 수 있도록 가공해주는 역할을 한다.
## MVC와 MVVM
MVC 패턴과 MVVM의 패턴은 거의 유사한데, 큰 차이점은 Controller라고 할 수 있다.

MVC에서는 Model의 데이터를 View에 맞게끔 Business Logic을 수행시키는 역할을 했다면...

MVVM은 역할을 ViewModel에 바로 넘겨주므로써 Controller의 역할을 줄일 수 있게 된 것으로 볼 수 있다!
## MVVM을 언제 사용하게 될까?
주로 MVVM은 데이터를 가공할 필요가 있을 경우에 사용하게 된다고들 한다.

만약 계산하는 로직을 짠다고 한다면, View Controller에서 계산하는 로직을 시행하는 MVC와는 달리, ViewModel에 역할을 넘겨주는 MVVM 패턴을 활용한다면 Controller의 역할을 줄일 수 있기 때문에 이러한 경우에 사용한다고 한다!

## MVVM 장점?
* MVVM은 View로부터 독립적
* View가 필요로 하는 데이터만 가지고 있음
* View와의 의존성 분리 가능
* 유지보수, 재사용성, 테스트 등을 용이하게 함
## MVVM 단점?
* View와 ViewModel의 양방향 binding 과정이 필요함
* 단순한 UI일 경우, MVVM 사용은 너무 과할 수 있음
* 앱이 커다래질수록 data binding이 복잡해짐

## 마지막으로.. MVVM을 사용할 때 주의할 점?
앱의 요구사항이 바뀐 기반으로 다른 디자인 패턴을 골라야 하는 경우도 존재하기 때문에 프로젝트 초기에 MVVM으로 바로 설계해버리는 것은 좋지 않을 수 있다고 생각한다.

___
이상으로 MVVM에 대한 공부를 마치도록 하겠다.