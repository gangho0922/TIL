 # MVC
 오늘은 MVC 패턴에 대해서 한번 배워볼 것이다.

 #### 그러기에 앞서!

 디자인 패턴이 무엇인지부터 먼저 알아보자.

 ## 디자인 패턴이란?
 공통의 문제에 검증된, 정형화된 개발 패턴으로, 지속적으로 효율적인 유지 보수, 지속적인 기능 개발과 효율성을 위한 템플릿이라고 보면 되겠다.

 이제 MVC 디자인 패턴에 대해서 알아보자!
___
## MVC란?
가장 기본적은 디자인 패턴이고 
Model - View - Controller의 줄임말로,
프로젝트를 구성할 때 그 구성 요소를 세가지의 역할로 구분한 패턴이다.
___
### Model
모델은 어플의 정보, 데이터를 나타내는 것으로, 데이터베이스, 초기화 값, 변수 등을 뜻한다. 이러한 DATA나 정보들의 가공시키는 것에 대한 책임을 맡고 있는 것이 바로 Model이다.

#### Model의 규칙
1. 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.

만약 내가 만들어 놓은 박스 안에 글자를 표시한다고 한다면, 박스의 위치, 박스의 크기, 글씨 크기, 글씨 위치, 글자 내용 등등의 정보를 가지고 있어야 된다는 것이다.

2. 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다.

데이터 변경이 일어났을 때 Model 내에서 화면 UI를 조정하기 위해 뷰를 참조하는 값을 가지면 안된다는 것이다.

3. 변경이 일어날 시, 변경 통지에 대한 처리 방법을 구현해야만 한다.

누가 모델을 변경하도록 하는 요청 이벤트를 보냈을 시, 이를 수신할 수 있는 처리 방법을 구현해야 하고, 모델은 재사용 가능해야만 하며 다른 인터페이스에서도 변하지 않아야 한다.
___
### View
데이터 및 객체의 입력 및 출력을 보여주는 담당을 하는 것으로, 데이터를 기반으로 사용자들이 볼 수 있는 화면을 뜻한다.

#### View의 규칙

1. 모델이 가지고 있는 정보를 따로 저장해서는 안된다.

화면에 박스를 그린다고 한다면 화면에 그리기만 한 뒤 화면에 그릴 때 필요한 정보를 저장하면 안된다.

2. 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 된다.

얘도 Model과 마찬가지로 자신을 빼고는 다른 요소를 참조하거나 어떻게 동작하는질 알아서는 안된다. 단지 화면에 표시해주는 역할만 있다고 생각하면 되겠다.

3. 변경이 일어나면 변경 통지에 대한 처리 방법을 구현해야만 한다.

화면에서 사용자가 화면에 표시된 내용을 변경하게 된다면 이를 모델에 전달해서 모델을 변경해야 된다는 것을 뜻한다.
___
### Controller
사용자가 데이터를 클릭하고, 수정하는 것에 대한 이벤트를 처리하는 담당을 하는 것이 바로 Controller이다.

#### Controller의 규칙

1. 모델이나 뷰에 대해서 알고 있어야 한다.

Model이나 View 같은 경우는 서로의 존재를 모르고 변경을 외부로 알려야 하는데 이를 Controller가 중재하기 위해서 모델과 그에 관련된 뷰에 대해서 알고 있어야 한다.

2. 모델이나 뷰의 변경을 모니터링 해야 한다.

모델이나 뷰의 변경 통지를 받을 시 이르 해석해 각각의 구성 요소에게 통지를 때려야 한다. 이로써 어플의 메인 로직은 Controller가 담당한다는 것을 알 수 있다.
___
### MVC 패턴을 사용해야 하는 이유
서로 분리되어 각자의 역할에 집중할 수 있게끔해서 개발을 하고 어플을 만든다면, 유지보수성, 어플의 확장성, 유연성이 증가하고, 중복 코딩이라는 문제점 또한 사라지게 하기 위해서 사용하는 것이 바로 MVC 패턴이다.

#### 왜 사용하는지 이제야 알았다!

___
이상으로 MVC 패턴에 대한 공부를 마치도록 하겠다.