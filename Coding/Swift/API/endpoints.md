# Endpoints



```swift
enum APIEndpoints {
    case createAccount
    case readInfo(id: Int)
    case updateAccount(id: Int)

    fileprivate var path: String {
        switch self {
            case .createAccount:
                return "/accounts"
            case .readInfo(let id):
                return "/into/\(id)"
            case .updateAccount(let id):
                return "/accounts/\(id)"
        }
    }

    var URL: Foundation.URL {
        var urlComponents = Servers.current.components
        urlComponents.path = urlComponents.path + path

        switch self {
            case .readInfo(_):
                let exampleQuery = URLQueryItem(name: "example", value: "something")
                urlComponents.queryItems = [exampleQuery]

            default:
                break
        }

        return urlComponents.url!
    }
}
```

