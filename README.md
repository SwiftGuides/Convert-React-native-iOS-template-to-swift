# Convert-React-native-iOS-template-to-swift
Steps below will convert objective c codes of ios module to swift

Source :- https://stackoverflow.com/a/48173122/12189609

### Steps:-

So after several tries i found out how to make it work with React Native 0.52

1 - Delete AppDelegate.m, AppDelegate.h and main.m

2 - Create a new AppDelegate.swift and when it asks if you would like to create an Objective-C bridge header just say "Yes"

3 - Copy the following to your Bridging-Header.h file:

```swift
#import <React/RCTBridgeModule.h>
#import <React/RCTBridge.h>
#import <React/RCTEventDispatcher.h>
#import <React/RCTRootView.h>
#import <React/RCTUtils.h>
#import <React/RCTConvert.h>
#import <React/RCTBundleURLProvider.h>
```

4 - Use the following code in your AppDelegate.swift file and edit the project name:

```swift
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
  var bridge: RCTBridge!

  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    let jsCodeLocation: URL

    jsCodeLocation = RCTBundleURLProvider.sharedSettings().jsBundleURL(forBundleRoot: "index", fallbackResource:nil)
    let rootView = RCTRootView(bundleURL: jsCodeLocation, moduleName: "YOUR-PROJECT-NAME", initialProperties: nil, launchOptions: launchOptions)
    let rootViewController = UIViewController()
    rootViewController.view = rootView

    self.window = UIWindow(frame: UIScreen.main.bounds)
    self.window?.rootViewController = rootViewController
    self.window?.makeKeyAndVisible()

    return true
  }
}
```
5 - Don´t forget to replace "YOUR-PROJECT-NAME" by your actual project name

6 - Run et voilà! Happy coding :)
