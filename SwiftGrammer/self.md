# self
### swift에서의 self란??
클래스나 구조체의 인스턴스 자신을 가르키는 것.
### 쓰는 형식
```swift
self.프로퍼티 명
```
여기서 프로퍼티 명을 구분해주는 .은 소속의 의미를 나타낸다.

인스턴스는 클래스의 외부에서만 접근 가능하기 때문에, 클래스 내부에서는 어느 인스턴스에 할당 될 것인지 알기 어렵다...

### 그래서!!!
이름 대신에 self 키워드를 사용해 자신의 인스턴스를 표현한다.

### self의 특징과 주의할 점
특징

> self는 생략이 가능하며, 실제로 많이 생략한다고 한다.

주의할 점
> 만약 프로퍼티와 일반 변수이름이 같다면 self를 사용하여 구분해주어야 함.

이상으로 self에 대한 소개를 마치도록 하겠다.