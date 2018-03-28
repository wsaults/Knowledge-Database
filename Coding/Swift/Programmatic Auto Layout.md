# Programmatic Auto Layout

> Note: A collection of notes from the [teamtreehouse.com](teamtreehouse.com) Programattic auto layout workshop.



## NSLayoutConstraint instances

> Note: It's best to create layout constraints in viewWillLayoutSubviews.

```swift
lazy var someView: UIView = {
    let view = UIView()
    
    // 
    view.translatesAutoresizingMaskIntoConstraints = false
    return view
}()

override func viewWillLayoutSubviews() {
    super.viewWillLayoutSubvies()
    
    let horizontalCenter = NSLayoutConstraint(item: someView,
            attribute: .centerX, relatedBy: .equal, toItem: view,
            attribute: .centerX, multiplier: 1.0, constant: 0)
    let someViewWidthConstraint = NSLayoutConstraint(item: someView,
            attribute: .width, relatedBy: .equal, toItem: nil, 
            attribute: .notAnAttribute, multiplier: 1.0, constant: 200)
    let someViewHeightConstraint = NSLayoutConstraint(item: someView,
            attribute: .height, relatedBy: .equal, toItem: nil, 
            attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
    let someViewBottomSpaceConstraint = NSLayoutConstraint(item: someView,
            attribute: .bottom, relatedBy: .equal, toItem: view,
            attribute: .bottom, multiplier: 1.0, constant: -50)
    
    NSLayoutConstraint.activate([
        horizontalCenter,
        someViewWidthConstraint,
        someViewHeightConstraint,
        someViewBottomSpaceConstraint
    ])
}
```



## NSLayoutAnchor

> Note: A factory class available in iOS 9

```swift
override func viewWillLayoutSubviews() {
    super.viewWillLayoutSubviews()
    
	NSLayoutConstraint.activate([
        someView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
        someView.widthAnchor.constraint(equalToConstraint: 200.0),
        someView.heightAnchor.constraint(equalToConstraint: 100.0),
        someView.bottomAnchor.constraint(equalTo: view.bottomAnchor, constant: -50.0)
	]) 
    
    // Layout guides and safe areas can be applied programatically as well.
}
```



## Visual format constraints

> Note: an early constraint solution and rarely used now.

```swift
// Ties views to a key
let views: [String: Any] = [
    "redView": redView,
    "greenView": greenView,
    "blueView": blueView
]

// Ties metrics to a key
let metrics: [String Any] = [
    "viewWidth": 200,
    "viewHeight": 200,
    "customVerticalSpacing": 50,
    "customHorizontalSpacing": 50,
] 

// The 'options' below let you specify alignment.

// Defines a horizontal width of 200 on the redView
// Spacing between the left and the view is 50
// 50 points between the redView and a greenView on the right
NSLayoutConstraint.constraints(withVisualFormat: "H:|-customHorizontalSpacing-[redView(viewWidth)]-customHorizontalSpacing-[greenView(viewWidth)]", options: [], metrics: metrics, views).map { $0.isActive = true }

// '|' Represents the superview
// '-' Represents the standard spacing of 8pts
NSLayoutConstraint.constraints(withVisualFormat: "V:|-customVerticalSpacing-[redView(viewHeight)]", options: [], metrics: metrics, views).map { $0.isActive = true }

// Sets the height of the greenView to the height of the redView
NSLayoutConstraint.constraints(withVisualFormat: "V:|-customVerticalSpacing-[greenView(redView)]", options: [], metrics: metrics, views).map { $0.isActive = true }
```

