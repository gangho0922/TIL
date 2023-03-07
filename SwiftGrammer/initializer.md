# initializer
## Swift의 initializer?
### 1. class 초기화-1
```swift
class SurveyQuestion{

    var text: String

    init(){

        self.text = "zedd"

    }

}

var question = SurveyQuestion()

print(question.text)//"zedd"
```
다음과 같이 init에 아무 파라미터를 안주고 직접 프로퍼티에 값을 줄 수 있다.