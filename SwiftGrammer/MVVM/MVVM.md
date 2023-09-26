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

MVVM은 