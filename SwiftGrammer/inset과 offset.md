# inset과 offset
swift에서 snapkit을 사용할 때 inset이나 offset을 많이 사용해봤을 것이다.

그런데 몇몇 나같은 초심자들은 offset과 inset의 차이점을 모를 때가 있다 ㅎ

그러므로 이번에 inset과 offset의 차이점에 대한 것을 알아보도록 하겠다!!

# offset
![Alt text](https://velog.velcdn.com/images/juh2/post/a1ac127b-aa76-4346-ad4c-2f519c876ec9/image.png)

위와 같이 offset은 위에 주황색을 예시로 들어서 저 superview로부터 기준을 잡아서 미는 형식이라고 생각하면 될 것 같다.
### 만약에!!
```swift
view.snp.makeConstraints {
    $0.bottom.right.equalToSuperview().offset(50)
}
```
이런식으로 코드를 작성한다면

![Alt text](https://velog.velcdn.com/images/juh2/post/f9763b35-20fb-4546-804c-f8b7361f9826/image.png)

위의 코드처럼 bottom과 right에 50씩 offset을 준다면 <br>
주황색을 위의 사진과 같이 아래로 50, 오른쪽으로 50 이동하는 것을 볼 수 있을 것이다.

# inset
inset은 padding을 주는 것과 같다고 생각하면 좋겠다.

### 만약!!
```swift
view.snp.makeConstraints {
    $0.top.left.right.bottom.equalToSuperview().inset(50)
}
```
다음과 같이 코드를 작성하게 된다면

![Alt text](https://velog.velcdn.com/images/juh2/post/0275038b-a9bc-4585-84c1-2e93ba78deb1/image.png)

위의 사진과 같이 top, left, right, bottom 모두 50씩 inset을 주게 된다면 <br>
네 방향 모두 50씩 padding이 들어가는 것을 볼 수 있을 것이다.

## 이렇게!
오늘은 inset과 offset의 차이점에 대해 한번 간단하게 알아보았다!

이전까지 쓸 때 무슨뜻인지도 모르고 쓸 때가 있었는데 이렇게 한번 알아보고 <br>
다져보기도 해서 기분이 후련하다!

이상 inset과 offset에 대한 차이점의 소개를 마치도록 하겠다.<br><br>
## 참고자료
https://velog.io/@juh2/SnapKit-offset-inset