# iOS: Path to Prod

## Setup
- Create dir
- init git & push 
```
git init && touch README.md && git add . && git commit -m "First commit" git remote add origin $url && git push -u origin master
```
- open xcode from dir `open -a Xcode`
- create project and push
- add cocoapods
  - `sudo gem install cocoapods`
  - `pod init`
  - Add the following to the podfile and then run `pod install`
```
# Podfile
platform :ios, '9.0'
use_frameworks!

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
- drop in .gitignore file and push
- open project and connect apple account
- launch project
- install [quick](https://github.com/Quick/Quick)/[nimble](https://github.com/Quick/Nimble)

## Testing
- outline simple AC
- Image
- background tap
- background color change
- lable change (shows text)
- create unit test and feature cycles

## Deploy
- setup [fastlane](https://fastlane.tools/)
- Automated test suite environment
  
## Pipeline
- CircleCi

## AppStore
- open apple dev web account
- generate certs
- create app in appstore connect
- add some info to the appstore connect
- put in ready to submit state

## AppStore Submission
- generate / update screen shots
- submit
