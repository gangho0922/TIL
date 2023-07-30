# Attribute
### Attribute란?
선언과 타입에 부가적인 정보를 제공하는 것이다.

### attribute 종류
* 선언에 적용되는 것
* type에 적용되는 것

### attribute를 사용한 형태
```swift
@attribute명(매개변수)
```
### 예시
함수 리턴 값을 꼭 사용 안해도 되게 하는 **@discardableResult**를 사용해보자!
```swift
@discardableResult func apple {
   return "sweet" 
}

apple()
```
___
이상으로 attribute에 대한 공부를 마치도록 하겠다.