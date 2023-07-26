# Realm
### Realm이란?
Realm은 모바일에 특화된 NoSQL 데이터베이스로 Swift, Objective-C, Java, Kotlin 등 다양한 SDK를 제공합니다.

iOS에서 Realm을 사용할 경우, UserDefaults와 CoreData를 대체해 Persistent data를 저장하고 관리할 수 있습니다.

대표적인 특징으로는 ORM이 아닌 데이터 컨테이너 모델을 사용하고, 데이터 객체를 Realm에 객체 형태로 저장합니다. 그렇기 때문에 DB에서 가져온 데이터를 복잡한 가공과정 없이 바로 사용할 수 있다는 장점이 있습니다.

### Realm의 특징
* SQLite와 CoreData보다 작업 속도가 빠르다.
*  Cross Platform을 지원해서 안드로이드 OS와 DB 파일을 공유할 수 있다.
*  Realm Studio를 통해서 DB 상태를 확인할 수 있다.
*  직관적인 코드로 작업할 수 있다.
*  Rx를 지원하는 RxRealm이 존재한다.

## Realm 사용 방법
### 1. 설치
Realm은 SPM, CocoaPods, Carthage 중 아무거나 사용해도 설치가 가능하다.
### 2. Model 정의해주기
예)
```swift
class PersonBook: Object {
    @Persisted(PrimaryKey: true) var residentNumber: String? // primary key로 지정
    @Persisted var name: String = ""
    @Persisted var status: String = ""

    convenience init(number: String) {
        self.init()
        self.residentNumber = residentNumber
    }
}
```
### 3. CRUD
Realm 데이터베이스에 접근하려면,
```swift
let realm = try! Realm()
```
이렇게 객체를 열어서 사용하면 된다.

### Create 부분
```swift
let personBook = PersonBook(residentNumber: "123456-0987654")

try! realm.write { 
    realm.add(personBook)
}
```
### Retrieve 부분
```swift
let books = realm.objects(PersonBook.self)

let predicateQuery = NSPredicate(format: "name = %@", "Ahn")
let result = savedShifts.books(predicateQuery)
```

### Update 부분
```
let toUpdate = books[0]

try! realm.write {
    books.name = "Kim"
}
```

### Delete 부분
```swift
let toDelete = book[0]

try! realm.write {
    realm.delete(toDelete)
}
```

이런 뉘양스로 CRUD를 작성하면 된다.

___
이상으로 Realm에 대한 공부를 마치도록 하겠다.