# UserDefaults
오늘은 UserDefaults에 대해 알아볼건데요. 제가 전에 하던 프로젝트에서 잠깐 했던거지만 그때는 자세히 알아보지 않고 그냥 막 써본거라...

### 그래서!!!

이번에 한번 제대로 공부해볼려고 합니다!

## UserDefaults란?
가장 기본적인 데이터베이스로 복잡하고 큰 용량의 데이터를 다루는데 유용하다고 하기보단 스위치 on, off 같이 간단한 데이터 저장에 유용하다고 보시면 될 것 같다.

UserDefaults의 데이터는 암호화 시켜서 저장시키는 것이 아니라 그대로 저장 시키기 때문에 보안과 관련된 정보를 저장하지 않았으면 한다.

만일, 앱이 삭제된다면 UserDefaults의 있는 데이터도 함께 사라지기 때문에 만일 데이터가 영구적으로 유지가 되야하는 식이라면 UserDefaults는 사용하지 않는 것이 좋을 것 같다!

### 그리고!!

UserDefaults는 싱글톤 객체라 스레드 안정성 또한 보장하기 때문에 데이터 동기화 문제를 고려하지 않아도 된다!

## 데이터 저장 방식
