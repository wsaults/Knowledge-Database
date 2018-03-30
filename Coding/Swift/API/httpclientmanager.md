# HTTPClientManager



```swift
import Freddy

class HTTPClientManager {
    var client = HTTPClient()
    
    // MARK: - Create
    
    func createAccount(email: String, password: String, confirmPassword: String,
                       completion: @escaping (Result<[String:Any]>) -> Void) {
        let url = APIEndpoints.createAccount.URL
        let body = JSON.dictionary([
                "account": .dictionary([
                        "email": .string(email),
                        "password": .string(password),
                        "password_confirmation": .string(confirmPassword)
                ])
        ])

        client.post(url: url, body: body) {
            data, response, error in

            DispatchQueue.main.async {
                if let _ = error {
                    completion(Result.failure(ResponseError.networkUnavailable))
                    return
                }

                guard let httpResponse = response as? HTTPURLResponse else {
                    return
                }

                if httpResponse.successful {
                    guard let data = data else {
                        return
                    }

                    do {
                        let json = try JSON(data: data)

                        let accountURLString = try json.getString(at: "account")
                        let accountURL = URL(string: accountURLString)!
                        let accountId = Int(accountURL.lastPathComponent)
                        let token = try json.getString(at: "auth_token")

                        completion(Result.success(["account": Account(id: accountId, email: email), "token": token]))
                    } catch {
                        completion(Result.failure(ResponseError.couldNotParseJSON))
                        return
                    }
                } else {
                    completion(Result.failure(self.parseError(data: data, response: httpResponse)))
                }
            }
        }
    }
    
    // MARK: - Read

    func readInfo(id: Int, completion: @escaping (Result<Info>) -> Void) {
        let url = APIEndpoints.readInfo(id: id).URL

        client.get(url: url) {
            data, response, error in

            DispatchQueue.main.async {
                if let _ = error {
                    completion(Result.failure(ResponseError.networkUnavailable))
                    return
                }

                guard let httpResponse = response as? HTTPURLResponse else {
                    return
                }

                if httpResponse.successful {
                    guard let data = data else {
                        completion(Result.failure(ResponseError.couldNotParseJSON))
                        return
                    }

                    do {
                        let json = try JSON(data: data)
                        let Info = try Info(json: json)

                        completion(Result.success(info))
                    } catch {
                        completion(Result.failure(ResponseError.couldNotParseJSON))
                        return
                    }
                } else {
                    completion(Result.failure(self.parseError(data: data, response: httpResponse)))
                }
            }
        }
    }
    
    // MARK: - Update
    
    func updateInfo(id: id, completion: @escaping (Result<Bool>) -> Void) {
        guard let infoId = id else {
            return
        }

        let url = APIEndpoints.updateInfo(id: infoId).URL

        client.put(url: url, body: info.putJSON()) {
            data, response, error in

            DispatchQueue.main.async {
                if let _ = error {
                    completion(Result.failure(ResponseError.networkUnavailable))
                    return
                }

                guard let httpResponse = response as? HTTPURLResponse else {
                    return
                }

                if httpResponse.successful {
                    completion(Result.success(true))
                } else {
                    completion(Result.failure(self.parseError(data: data, response: httpResponse)))
                }
            }
        }
    }
}
```

