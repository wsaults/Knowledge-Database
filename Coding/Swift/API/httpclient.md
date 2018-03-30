# HTTPClient



```swift
import Freddy

typealias DataTaskResult = (Data?, URLResponse?, Error?) -> Void

protocol URLSessionDataTaskProtocol {
    func resume()
}

protocol URLSessionProtocol {
    func dataTaskWithRequest(request: URLRequest, completionHandler: @escaping DataTaskResult) -> URLSessionDataTaskProtocol
}

class HTTPClient {
    var session = Session.sharedInstance
    var urlSession: URLSessionProtocol!
    private var authToken: String? {
        return session.authToken
    }
    
    private var registrationToken: String? {
        return session.customer.registrationToken
    }
    
    init() {
        let sessionConfiguration = URLSessionConfiguration.default
        let timeout: TimeInterval = 12
        sessionConfiguration.timeoutIntervalForRequest = timeout
        sessionConfiguration.timeoutIntervalForResource = timeout
        let urlSession = URLSession(configuration: sessionConfiguration)
        
        self.urlSession = urlSession
    }
    
    func get(url: URL, completion: @escaping DataTaskResult) {
        sendRequest(url: url, method: "GET", body: nil, completion: completion)
    }
    
    func delete(url: URL, completion: @escaping DataTaskResult) {
        sendRequest(url: url, method: "DELETE", body: nil, completion: completion)
    }
    
    func put(url: URL, body: JSON?, completion: @escaping DataTaskResult) {
        sendRequest(url: url, method: "PUT", body: body, completion: completion)
    }
    
    func post(url: URL, body: JSON?, completion: @escaping DataTaskResult) {
        sendRequest(url: url, method: "POST", body: body, completion: completion)
    }
    
    private func sendRequest(url: URL, method: String, body: JSON?, completion: @escaping DataTaskResult) {
        var request = URLRequest(url: url)
        request.httpMethod = method
        
        var jsonData: Data?
        if let body = body {
            do {
                jsonData = try body.serialize()
            } catch {
                return
            }
            
            request.httpBody = jsonData
        }
        
        sendRequest(request: request, completion: completion)
    }
    
    private func sendRequest(request: URLRequest, completion: @escaping DataTaskResult) {
        var headers: [String:String] = ["Content-Type": "application/json"]
        if let authToken = authToken {
            headers["x-auth-token"] = authToken
        }
        
        if let registrationToken = registrationToken {
            headers["x-registration-token"] = registrationToken
        }
        
        var mutableRequest = request
        mutableRequest.allHTTPHeaderFields = headers
        
        let task = urlSession.dataTaskWithRequest(request: mutableRequest, completionHandler: completion)
        
        task.resume()
    }
}

extension URLSessionDataTask: URLSessionDataTaskProtocol {
}

extension URLSession: URLSessionProtocol {
    func dataTaskWithRequest(request: URLRequest, completionHandler: @escaping DataTaskResult) -> URLSessionDataTaskProtocol {
        return dataTask(with: request, completionHandler: completionHandler) as URLSessionDataTask as URLSessionDataTaskProtocol
    }
}

extension HTTPURLResponse {
    var successful: Bool {
        return (200 ... 299).contains(statusCode)
    }
}
```

