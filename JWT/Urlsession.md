# Urlsession?
## Urlsession이란?
네트워크 데이터 전달 작업에 연관된 일련의 일을 처리하는 그룹 오브젝트이다. <br>
URLSession 클래스 및 관련 클래스들은 URLs에 의해 표현되는 엔드포인트에 데이터를 업로드하거나, 다운로드할 수 있도록 하는 API를 제공한다. 또한 URLSession을 통해 iOS 앱이 실행중이지 않을 때에도 백그라운드에서 데이터를 다운로드할 수 있다. <br>
URLSessionDelegate나 URLSessionTaskDelegate를 사용하여 일의 완료(task completion)나 redirection과 같은 이벤트 또는 authentication(인증-로그인 또는 회원가입)을 지원할 수 있다. <br>
본격적으로 URLSession에 대해 알아보기에 앞서, 우리는 URL Loading System에 대해 알 필요가 있다.

## Urlsession 사용법

**URLSession을 이용한 네트워킹 구현순서**
- URL 만들기
- URLSession 구성하기
- dataTask 만들기
- 네트워크 요청완료 핸들러 처리하기

## 1. URL 만들기

URL(string:)을 이용해서 String타입의 주소를 URL로 바로 만들어서 사용해도 되지만 String을 하드코딩해서 다루는 것은 단점이 많습니다. REST API의 url 설계구조를 감안하면 아래의 이미지의 구조로 나눠서 관리하는 것이 더 좋습니다. 

![](https://kirkim.github.io/assets/img/swift/urlsession/1.png)

URLComponents를 이용하면 좀 더 명확하게 관리를 해줄 수 있습니다.
```swift
struct NetworkAPI {
    static let schema = "https"
    static let host = "api.unsplash.com"
    static let path = "/photos"

    func getRandomImageAPI(page: Int) -> URLComponents {

        var components = URLComponents()
        components.scheme = NetworkAPI.schema
        components.host = NetworkAPI.host
        components.path = NetworkAPI.path

        components.queryItems = [
            URLQueryItem(name: "client_id", value: "xxxxxxxxx"),
            URLQueryItem(name: "count", value: "15"),
            URLQueryItem(name: "page", value: String(page))
        ]
        return components
    }
}
```

URLComponents의 .url요소에 접근하여 조립된 URL값을 옵셔널형태로 얻을 수 있습니다.
```swift
let url = api.getRandomImageAPI(page: page).url
```
___
## 2. URLSession 구성하기

URLSession은 싱글톤(shared)으로 만들어 줄 수 있는데, 사용자 정의는 할 수 없기 때문에 간단한 기본 요청에 대한 처리로 사용하면 될 것 같습니다.
```swift
URLSeeion.shared
```
다른 방법으로 직접 URLSessionConfiguration을 설정해서 만들어줄 수 있습니다.

- .default: 싱글턴(share)과 비슷하게 작동하지만 delegate를 이용하여 데이터를 점진적으로 얻을 수 있습니다.
- .ephemeral: 캐시, 쿠키 또는 자격증명을 디스크에 저장하지않을때 사용하는 임시세션입니다.
- .background(withIdentifier:): 앱이 실행되지 않는 동안 백그라운드에서 콘테츠를 업로드 및 다운로드작업을 수행할 수 있습니다.
___

기본세션인 .default를 이용해서 세션을 만들어 줬습니다.
```swift
class URLSessionManager {
    static let shared = URLSessionManager()
    private let session = URLSession(configuration: .default)
    private let api = NetworkAPI()

    private init() { }
	// 코드 생략
}
```
___
## 3. Task 만들기

위에서 만들어준 URLSession을 이용해서 Task를 만들 수 있습니다.

- Data Task: NSData 객체를 이용해서 통신합니다. 짧은 대화형 요청을 위한 것입니다.(GET)
- Upload Task: Data task와 비슷하지만 파일형태의 데이터도 보내며, 백그라운드 통신도 지원합니다.(POST, PUT)
- Download Task: 데이터를 다운로드(파일형태도가능)를 하며, 백그라운드 통신도 지원합니다.
- WebSocket Task: RFC 6455에 정의된 WebSocket프로토콜을 사용하여 TCP 및 TLS를 통해 메시지를 교환

이번에는 간단한 JSON타입으로 만들 data이므로 Data Task를 이용하여 만들어줄 예정입니다.

## url vs request

Task는 URL or URLRequest로 만들어줄 수 있습니다.<br>
URLRequest를 이용하면 HttpMethod와 Http헤더를 설정해줄 수 있습니다.<br>
사실 HttpMethod의 기본값은 GET으로 세팅되어 있고, 필수적인 Http헤더(Content-Length, Authorization, Connection, Host…)는 이미 세팅되어 있습니다. 그렇기 때문에 단순히 GET요청일 경우 URL로 dataTask를 만들어 사용해도 됩니다.<br>
가끔, Authorization와 같이 인증키가 GET요청을 할때 필요할 수 있습니다. 이때는 GET요청일때도 URLRequest를 이용해서 dataTask를 만들어 세팅해주면 됩니다. POST요청의 경우 반드시 URLRequest로 Task를 만들어서 아래 코드와 같은 세팅이 필요합니다.<br>
```swift
var request = URLRequest(url: url)

request.httpMethod = "POST"
request.setValue("application/x-www-form-urlencoded", forHTTPHeaderField: "Content-Type")
request.setValue("application/json", forHTTPHeaderField: "Accept")
```

이번 포스트에서는 따로 헤더를 세팅할 필요가없는 GET요청이기 때문에 아래와 같이 URL을 그대로 사용해서 dataTask를 만들어 줬습니다.

```swift
func getImageInfo(page: Int, completion: @escaping (Result<[ImageInfo], CustomError>) -> ()) {
    guard let url = api.getRandomImageAPI(page: page).url else {
        completion(.failure(CustomError.makeURLError))
        return
    }

    session.dataTask(with: url) { data, response, error in
        ...
    }.resume()
}
```
## 4. 네트워크 요청완료 핸들러 처리하기

네트워킹이 끝나면 completion(핸들러, 비동기)형태로 응답값을 받을 수 있습니다. 읍답값은 다음과 같이 Data, URLResponse, Error의 옵셔널형태로 구성되어 있습니다. 다음일때 실패처리를 했습니다.

1. error값이 존재할 때
2. response의 상태코드값이 200번대가 아닐 때
3. data값이 없을 때
   
자세한 에러처리 방법은 에러핸들링하기 포스트 - kirkim를 참고해주세요. data값이 존제하는 것을 최종적으로 확인하게 되면, JSONDecoder()를 이용해서 원하는 타입으로 디코딩을 해주면 됩니다.
```swift
session.dataTask(with: url) { data, response, error in
    guard error == nil else {
        completion(.failure(.error(error: error)))
        return
    }
    if let httpResponse = response as? HTTPURLResponse,
       !(200...299).contains(httpResponse.statusCode) {
        completion(.failure(.responseError(code:httpResponse.statusCode)))
        return
    }
    guard let data = data else {
        completion(.failure(.noData))
        return
    }
    /* 코드 생략 */
}.resume()
```
___
## Decodable 데이터 타입만들기

data(Data타입)이 nil값이 아닌 것 까지 확인하면 원하는 타입으로 디코딩(decoding)하는 과정이 필요합니다. Decodable을 준수하면 디코딩이 가능한 타입이 됩니다.

- Decodable: 디코딩가능한 타입
- Encodable: 인코딩가능한 타입
- Codable: Decodable + Encodable
아래의 코드는 이번에 사용한 데이터 타입니다. 필요한 요소만 선택해서 구성할 수 있으며 다계층구조로도 구현할 수 있습니다.<br><br>
**단, JSON타입의 key값과 데이터타입은 올바르게 적어야 합니다.**<br><br>
만약 원하는 변수명으로 사용하고 싶다면 CodingKey프로토콜 을 이용하면 됩니다.이때, enum 타입명도 반드시 CodingKeys로 만들어 줘야 합니다.
```swift
struct ImageInfo: Decodable {
    var updatedAt: String
    var imageURL: ImageURL
    var author: Author
    var likes: Int
    var width: Int
    var height: Int

    private enum CodingKeys: String, CodingKey {
        case updatedAt = "updated_at"
        case imageURL = "urls"
        case author = "user"
        case likes, width, height
    }
}
```

이제 다음과 같이 JSONDecoder()를 이용해여 디코딩을 해주면 됩니다. 실패시 Error를 throw하므로 try-catch문으로 만들어줍니다.

```swift
do {
    let hasData = try JSONDecoder().decode([ImageInfo].self, from: data)
    completion(.success(hasData))
} catch let error as NSError {
    completion(.failure(.decodingError(error: error)))
}
```

## 5. NetworkManager 전체코드
```swift
import Foundation

final class NetworkManager {
    static let shared = NetworkManager()
    private init() { }

    private let api = NetworkAPI()
    private let session = URLSession(configuration: .default)

    func getImageInfo(page: Int, completion: @escaping (Result<[ImageInfo], CustomError>) -> ()) {
        guard let url = api.getRandomImageAPI(page: page).url else {
            completion(.failure(CustomError.makeURLError))
            return
        }

        session.dataTask(with: url) { data, response, error in
            guard error == nil else {
                completion(.failure(.error(error: error)))
                return
            }
            if let httpResponse = response as? HTTPURLResponse,
               !(200...299).contains(httpResponse.statusCode) {
                completion(.failure(.responseError(code:httpResponse.statusCode)))
                return
            }
            guard let data = data else {
                completion(.failure(.noData))
                return
            }
            do {
                let hasData = try JSONDecoder().decode([ImageInfo].self, from: data)
                completion(.success(hasData))
            } catch let error as NSError {
                completion(.failure(.decodingError(error: error)))
            }
        }.resume()
    }
}
```
이런 식으로 urlsession을 사용하여 코드를 짤 수 있습니다!

추가 참고 링크 -> [Click](https://gyuios.tistory.com/108) <br>
이상으로 urlsession에 대한 내용을 마치도록 하겠습니다.