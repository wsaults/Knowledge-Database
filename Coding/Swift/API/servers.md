# Servers

```swift
enum Servers {
    static var current = Servers.prod

    case prod
    case dev
    case localhost

    var components: URLComponents {
        var urlComponents = URLComponents()
        urlComponents.scheme = self.scheme
        urlComponents.path = self.path!

        let baseHost = ".mysite.com"

        switch self {
            case .prod:
                urlComponents.host = "app\(baseHost)"
            case .dev:
                urlComponents.host = "dev\(baseHost)"
            case .localhost:
                urlComponents.host = "localhost"
                urlComponents.port = 3000
        }
        return urlComponents
    }

    fileprivate var scheme: String {
        switch self {
            case .localhost:
                return "http"
            default:
                return "https"
        }
    }

    fileprivate var path: String? {
        return "/api"
    }
}
```
