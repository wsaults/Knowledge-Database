# iOS: Path to Prod

## Prerequisites:
- iOS Developer account
- XCode 9 or greater
- Brew
- Cocoapods
- Text editor (I'm using vs code here)
- Github
- Slack channel & app


## Setup
- Create XCode project with Unit and UITests options checked.
- init git & push 
```
git init && touch README.md && git add . && git commit -m "First commit" && git remote add origin [$url] && git push -u origin master
```
- add cocoapods for [quick](https://github.com/Quick/Quick)/[nimble](https://github.com/Quick/Nimble)
  - `sudo gem install cocoapods`
  - `pod init`
  - Update your podfile `code . Podfile` to include the following and then run `pod install`
  ```
  def testing_pods
      pod 'Quick'
      pod 'Nimble'
  end

  target '$TEST_TARGET_NAME' do
      testing_pods
  end

  target '$UITEST_TARGET_NAME do
      testing_pods
  end
  ```
  - touch .gitignore file `touch .gitignore && code . .gitignore`, update with the following
  ```
  xcuserdata/
  */xcshareddata/
  *.ipa
  *.dSYM.zip
  *.dSYM
  fastlane/report.xml
  fastlane/Preview.html
  fastlane/screenshots/**/*.png
  fastlane/test_output
  .env.default
  ```
  ...then push:
  ```
  git add . && git commit -m "added pods and ignore file" && git push
  ```
- open xcworkspace using `open *.xcworkspace`
- [code signing](use_automatic_signing)

## Testing
- outline simple AC
- Image
- background tap
- background color change
- lable change (shows text)
- create unit test and feature cycles

## Deploy
- setup [fastlane](https://fastlane.tools/) using the [docs](https://docs.fastlane.tools/)
  - `fastlane init`
  - Prepare a repo for [match](https://docs.fastlane.tools/actions/match/)
  - `fastlane match init`
  - `fastlane match development --readonly`
  - `fastlane match appstore --readonly`
  - `fastlane snapshot init` and Add the `./fastlane/SnapshotHelper.swift` to your UI Test target
  - add the following to your UI test:
  ```
  let app = XCUIApplication()
  setupSnapshot(app)
  app.launch()
  ```
  - use: `snapshot("0Launch")` to wherever you want to trigger screenshots
  - `code . Fastfile` and add the following:
  ```
  // WIP
  
  lane :release do
    capture_screenshots
    build_app
    upload_to_app_store       # Upload the screenshots and the binary to iTunes
    slack                     # Let your team-mates know the new version is live
  end
  
  lane :test do
    run_tests(scheme: "testDemoApp")
  end
  
  desc "Deploy a new version to the App Store"
  lane :release do
    # match(type: "appstore")
    # snapshot
    increment_build_number
    gym # Build your app - more options available
    sigh
    deliver(
      skip_screenshots: true,
      skip_metadata: false,
      submit_for_review: false,
      automatic_release: true)
    # frameit
  end
  ```
  - Edit the project scheme, mark it as `shared`, and check the `run` boxs under `build`
  
## Pipeline
- [CircleCi](https://circleci.com/)

## AppStore
- open [apple dev](https://developer.apple.com/) web account
- create app in appstore connect
- add some info to the appstore connect
- put in ready to submit state

## AppStore Submission
- generate / update screen shots
- Automated version with [agvtool](https://developer.apple.com/library/archive/qa/qa1827/_index.html)
  - Set the `Current Project Version` under `Build Settings` for each target
  - Set `Versioning System` to `Apple Generic` to ensure that Xcode will include all agvtool-generated version information in your project.
- submit
