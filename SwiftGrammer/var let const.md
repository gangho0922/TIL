# var, let 그리고 const
Swift의 변수선언에는 var과 let과 const가 있다.

이 세가지의 선언방식들의 차이점에 대해 한번 알아보자!
## 변수선언 방식
우선 var의 변수 선언방식에는 큰 단점이 있다.
```swift
var name = 'Gangho'
    console.log(name) 
    // Gangho

    var name = 'Kangho'
    console.log(name) 
    // Kangho
```
다음과 같이 변수를 한번 더 선언 했음에도 에러가 나오지 않고 각각 다른 값들이 출력되는 것을 볼 수 있다.

이는 간단한 코드량에선 우리에게 편리함을 가져다 줄 수 있겠지만 만약 코드량이 많아진다면 어디에서 어떻게 사용되는지 알기 힘들고 값이 되려 바뀔 수도 있다.

한번 위의 변수선언 방식에서 let을 활용하여 다음과 같이 한번 바꿔보자!
```swift
let name = 'Gangho'
    console.log(name) 
    // Gangho

    let name = 'Kangho'
    console.log(name) 
    // Uncaught SyntaxError: Identifier 'name' has already been declared
```
다음과 같이 코드를 짜게 된다면, 다음코드의 아래 주석 처럼 name이 이미 선언되었다는 에러 메세지가 나오게 된다.(const도 똑같다.)

그럼 여기서 let과 const의 차이점은 과연 무엇일까?

바로...이 둘의 차이점은 immutable 여부이다!!!
```swift
let name = 'Gangho'
    console.log(name) 
    // Gangho

    let name = 'Kangho'
    console.log(name) 
    // Uncaught SyntaxError: Identifier 'name' has already been declared
    name = 'AnnKangho'
    console.log(name)
    // AnnKangho
```
let은 다음과 같이 변수에 재할당이 가능하다. 하지만!!
```swift
const name = 'Gangho'
    console.log(name) 
    // Gangho

    const name = 'Kangho'
    console.log(name) 
    // Uncaught SyntaxError: Identifier 'name' has already been declared
    name = 'AnnKangho'
    console.log(name)
    //Uncaught TypeError: Assignment to constant variable.
```
const는 다음과 같이 변수 재선언, 변수 재할당 모두 불가능하다...

## 호이스팅
#### 호이스팅이란?
var 선언문이나 function 선언문 등을 해당 스코프의 선두로 옮긴 것처럼 동작하는 특성을 말한다.

자바스크립트는 let, const를 포함하여 모든 선언(var, let const, function, function*, class)을 호이스팅한다.

하지만!!

var로 선언된 변수와는 달리 let으로 선언된 변수를 선언문 이전에 참조하면 참조에러가 발생하게 된다.
```swift
console.log(foo); // undefined
	var foo;

	console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
	let bar;
```
이는 let으로 선언된 변수는 스코프의 시작에서 변수의 선언까지 일시적으로 사각지대에 빠지기 때문이다.

> 참고⭐️

> [변수 생성 과정]
    <br>
선언 단계 > 초기화 단계 > 할당 단계
```swift
// 스코프의 선두에서 선언 단계와 초기화 단계가 실행된다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 있다.

console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```
var으로 선언된 변수는 선언단계와 초기화 단계가 한번에 이루어진다.
```swift
// 스코프의 선두에서 선언 단계가 실행된다.
// 아직 변수가 초기화(메모리 공간 확보와 undefined로 초기화)되지 않았다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 없다.

console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```
let으로 선언된 변수는 선언 단계와 초기화 단게가 분리되어 진행된다.

## 정리
변수 선언에는 기본적으로 const를 사용하고, 재할당이 필요할 경우 한정해 let을 사용하는 것이 좋다!

const를 사용하면 의도치 않은 재할당을 방지해 주기 때문에 보다 안전하다는 것 알아둬라!

재할당이 필요할 경우 let을 사용하는데 이때 변수의 스코프는 최대한 좁게 만든다.

재할당이 필요 없는 상수와 객체에는 const 사용!

참조문서 <br>
Click [here](https://velog.io/@bathingape/JavaScript-var-let-const-차이점)

이상으로 var let const의 차이점에 대한 소개를 마치도록 하겠다!