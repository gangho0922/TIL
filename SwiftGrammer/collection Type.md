# Collection Type
## 컬렉션 타입이란?
데이터들의 집합소라고 보면 되는데 지정된 타입들을 하나로 묶은 형태라고 보면 된다! 

모든 프로그래밍 언어에서 데이터들을 한번엔 관리할 수 있고 쉽게 사용할 수 있게 하기 위해 컬렉션 타입은 필수적이다.

Swift의 컬렉션 타입에는 배열(Array), 딕셔너리(Dictionary), 세트(Set)가 있다!

한번 차례차례 배열부터 알아보자.
## 1. 배열
Swift에서 배열은 같은 데이터 타입의 값들을 순서대로 저장하는 리스트이다. 즉 데이터들의 집합이라고 보면 된다! 배열에는 순서가 있이 저장이 되어 어떠한 요소에 접근하기 매우 편리하다. 배열에 대한 코드를 아래에 한번 적어보도록 하겠다!
```swift
var color : Array<String> = ["red", "orange", "yellow", "green", "blue"]
var number : [Int] = [10, 8, 3, 7]
// 배열 선언

color += ["dark"]
number.append(99)
// 배열에 요소 추가하는 방법

print(color[0])
print(color[3])
print(color.first) // 첫번째 요소
print(color.last) // 마지막 요소
// 배열 접근

let Backup = color
print(Backup)
// 배열 복사
```
문자열 배열 하나와 정수형 배열 하나 총 두가지 배열을 선언해 보았습니다. 여기서 알 수 있듯이 배열을 배열을 선언하는 방법에는 크게 두가지가 있다.
```swift
var number : Array<Int> = [10, 8, 3, 7]
var number : [Int] = [10, 8, 3, 7]
```
두 코드 다 같은 선언방법이니 아무거나 편한걸로 사용하면 되겠다!

배열에 데이터를 추가하는 방법은 배열에는 순서대로 저장되기 때문에 +=을 써서 마지막에 데이터를 저장해 줄 수 있고, append함수를 이용해서 마지막에 데이터를 추가해 줄 수 있다!

그리고 배열은 index를 통해서 접근할 수 있다! 배열[index]로 해당 인덱스에 접근이 가능하고 .fist나 .last로 사용하여 각각 첫번째와 마지막 요소에 접근도 가능하다! 

배열은 그대로 복사도 가능한데 아주 간단한게 =을 사용해서 복사를 할 수 있다!

그럼 맨위에 있었던 코드를 다시 한번 봐보자!
```swift
var color : Array<String> = ["red", "orange", "yellow", "green", "blue"]
var number : [Int] = [10, 8, 3, 7]
// 배열 선언

color += ["dark"]
number.append(99)
// 배열에 요소 추가하는 방법

print(color[0])
print(color[3])
print(color.first) // 첫번째 요소
print(color.last) // 마지막 요소
// 배열 접근

let Backup = color
print(Backup)
// 배열 복사
```
실행하게 될 시
```
red
green
Optional("red")
Optional("dark")
["red", "orange", "yellow", "green", "blue"]
```
다음과 같이 뜨게 되는데 .first와 .last로 쓰게 될 시 다음과 같은 경고 오류가 발생하게 된다..
```
Expression implicitly coerced from 'String?' to 'Any
```
인덱스 결과에서는 잘 뜬것으로 보이지만 .first와 .last부분의 결과는 Optional 이라 뜨면서 우리가 예상 했던 red 값이 나오는게 아니였다! 이 부분은 optional에 대한 포스팅을 참고해주시길 바란다!
## 2. 딕셔너리
Swift에서 딕셔너리는 순서없이 키와 값을 한 쌍으로 데이터를 저장하는 컬렉션 타입이다.
```swift
var namedic : [String : Int] = ["song":4, "kim":8, "kang":15, "park":8, "choi":4]

//딕셔너리 추가
namedic["dong"]=10 

//key값과 value값
print(namedic.keys)   //딕셔너리의 키값들
print(namedic.values) //딕셔너리의 값들

//딕셔너리 접근
print(namedic["song"])
print(namedic["kang"])

//딕셔너리의 키를 배열로 가져오기
let namestr = [String](namedic.keys) 
print(namestr)
```
딕셔너리도 배열과 비슷하다!

대신 딕셔너리 안에는 키값과 value값이 존재하고 하나의 키값에 하나의 value값이 할당이 되는 형태로 이루어져 있다.

새로운 키값을 추가할 때는 [새로운 키값]=value형식으로 추가하면 되고 .keys와 .value를 이용하여 키값과 value값을 확인할 수 있다.

접근하는 방법으로는 namedic["song"]으로 접근이 가능했고 키값과 value값을 배열로 변환도 할 수 있는 것을 확인 할 수 있었다.
## 세트
Swift에서 세트는 같은 데이터 타입의 값들을 순서없이 저장하는 리스트이다. 순서가 없다는 점만 빼면 배열과 비슷한데, 세트에서는 순서가 없기 때문에 서로 같은 값들을 구분 할 수 없다.그래서 세트에서는 중복된 값은 허용되지 않는다!
```swift
let subway : Set = ["시청", "을지로", "방배", "용산", "이촌", "성수"]
var subway2 : Set = ["용산", "대화", "오금", "대치", "강남", "성수"]

//교집합을 새로운 set으로 만들어줌
let transfer = subway2.intersection(subway) 
print(transfer)

//subway2에서 차집합을 새로운 set으로 만들어줌
let nottransfer = subway2.subtracting(subway) 
print(nottransfer)

//합집합을 새로운 set으로 만들어줌
let union = subway2.union(subway) 
print(union)

subway2.insert("군자") 
print(subway2)
subway2.remove("군자") 
print(subway2)
```
Set에서는 순서가 없고 인덱스가 없으며 중복을 허용하지 않기 때문에 다양한 함수를 사용가능하다!

여기서 상식⭐️
> .intersection -> 두 세트에 대해 교집합을 새로운 세트로 만들어줌.

> .subtracting -> 두 세트에 대해 차집합을 새로운 세트로 만들어줌.

> .union -> 두 세트에 대해 합집합을 새로운 세트로 만들어줌.

세트를 사용할 때 이러한 집ㅎ팝 형식을 이용하면 더 편히 사용할 수 있다.

세트의 요소 추가는 .insert로,<br>
요소 삭제는 .remove를 이용하는 것을 알 수 있다!
![출력이미지](https://velog.velcdn.com/images%2Fwook4506%2Fpost%2F1244564f-6ff0-4600-b248-6b7273f8a13b%2F스크린샷%202021-05-06%20오후%203.18.41.png)
실행 시켜보면 다음과 같이 잘 출력되는 것을 알 수 있다.

이상으로 collection type에 대한 소개를 마치도록 하겠다!