# QuickSpec



### Setup

```swift
@testable import project_name

class ClassNameViewControllerSpec: QuickSpec {
    override func spec() {
        describe("ClassNameViewController") {
            var subject: ClassNameViewController!
            
            beforeEach {
                let storyboard = UIStoryboard(name: "Main", bundle: nil)
                subject = storyboard.instantiateInitialViewController(withIdentifier: "ClassNameViewController") as! ClassNameViewController
                
                subject.view.layoutSubviews()
            }
        }
	}
}
```

> Note: Be sure to set the identifier for the viewController in the storyboard.

