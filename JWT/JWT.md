# JWT
## JWT란?
JWT란 Json Web Token의 약자로, 모바일이나 웹의 사용자 인증을 하기 위해서 사용되는 암호화된 토큰을 의미한다.

## JWT가 담는 정보
JWT는 header / payload / signature

세파트로 나뉘어지는데, 각 파트는 .으로 구분해서
```
aaaaa.bbbbb.ccccc
```
이런식으로 표현된다.<br>
JWT는 URL에서 파라미터로 이동할 수 있도록<br>
URL_Safe한 Base64url 인코딩을 한다.

여기서!

Base64 인코딩?
이것은 Binary 데이터를 텍스트로 바꾸는 인코딩이다.<br>
이 인코딩 방식은 Binary 데이터를 6bit씩 자른 후 해당되는 문자열을 ASCII 값으로 치환해주는 방식이다.

이제 앞서 말했던 세 파트

**header / payload / signature**

이것들에 대해 하나하나 알아보도록 하겠다!

## 1. header
```swift
{
  "typ": "JWT",
  "alg": "HS256"
}
```
위와 같이 header는 토큰의 타입과 해시 암호화 알고리즘으로 구성된다.
## 2. payload
```swift
{
  "sub": "1234567890", // 등록된 플레임
  "name": "John Doe", // 비공개 플레임
  "iat": 1516239022  // 등록된 플레임
}
```
위와 같이 토큰에 담을 정보가 들어있고, 여기에 담은 정보를 한 '조각'을 클레임이라고 부른다. 이는 name/value의 한쌍으로 이루어져 있다.

클레임의 종류
* 등록된 클레임
* 공개 클레임
* 비공개 클레임

## 3. signature
signature는 [header base64 + payload base64 + SECRET_KEY]를 사용하여 JWT 백엔드에서 발행된다.

각 요청 시 서명이 확인되고, header 또는 payload의 정보가 클라이언트에 의해 변경된 경우에는 signature가 무효화 된다.