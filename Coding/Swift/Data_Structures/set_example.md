# An Example set implementation in Swift

```swift
class Set: NSObject {
    
    var data: [String]?
    
    override init() {
        super.init()
        
        data = []
    }
    
    func length() -> Int {
        return data?.count ?? 0
    }
    
    func add(_ value: String) {
        self.data?.append(value)
    }
    
    func remove(_ value: String) {
        guard let index = self.data?.index(of: value) else {
            return
        }
        
        self.data?.remove(at: index)
    }
    
    func contains(_ value: String) -> Bool {
        return self.data?.contains(value) ?? false
    }
}

let set = Set()
set.add("Wubba lubba dub dub!")
set.length()                            // Returns 1
set.contains("Wubba lubba dub dub!")    // Returns true
set.remove("Wubba lubba dub dub!")
set.length()                            // Returns 0
set.contains("Wubba lubba dub dub!")    // Returns false
```