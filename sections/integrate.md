---
title: Skafos Integration

---
# Skafos Integration
Follow these steps to integrate Skafos with your iOS application. For a more detailed set of instructions,
tailored to your application and model, visit the [dashboard](https://dashboard.skafos.ai).

## Install Skafos Framework

### CocoaPods

To integrate Skafos into your Xcode project using CocoaPods, specify it in your [Podfile](https://guides.cocoapods.org/syntax/podfile.html):
```
pod 'Skafos', '~> 4.0.3'
```

Install the framework:
```
$ pod install
```
Or, run `pod update` if you've already setup your pod environment and your just making a change to the Podfile.

### Carthage

To integrate Skafos into your Xcode project using Carthage, specify it in your [Cartfile](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#cartfile):
```
github 'skafos/ios' '4.0.3'
```

Install the framework:
```
$ carthage update
```

**After installing Skafos, open the Xcode workspace:**
```
$ open <your-app>.xcworkspace/
```

## Import Skafos

Inside your app delegate and view controller, add the following:

```swift
import Skafos
```

## Set Environment Keys

Embed the `Skafos.initialize` method with your environment keys in the `AppDelegate.swift` file:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:
    [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

  // Set Skafos environment keys
  // You can find them under your App Settings tab @ https://dashboard.skafos.ai
  #if DEBUG
    // Use the DEV key if running in DEBUG mode
    let key = "{your-dev-key}"
  #else
    // Use the PROD key otherwise
    let key = "{your-prod-key}"
  #endif

  // Initialize Skafos
  Skafos.initialize(key, swizzle: true)

  return true
}
```

## Setup Model Version Updates

In order to receive model updates over the air, embed the `Skafos.load` method in your
view controller and change `MyCustomModel()` to match your CoreML model name and `modelName` to
match the model name you assigned in the dashboard.

```swift
import UIKit
import Skafos

class MainViewController : UIViewController {
    // This is the model name you assigned on the dashboard
    private let modelName:String = "<your-skafos-model-name>"

    // CoreML automatically uses the name of your .mlmodel file as the class name
    // e.g. MyCustomModel.mlmodel --> MyCustomModel()
    private let myModel = MyCustomModel()

    // Check for model updates when UI view appears
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)

        // Load a new version of your model if available
        Skafos.load(asset: self.modelName) { (error, asset) in
            // Log the asset in the console
            console.info(asset)
            guard error == nil else {
                console.error("Error: \(String(describing: error))")
                return
            }
            if let model = asset.model {
                // Assign the updated model
                self.myModel.model = model
            }
        }
    }
}
```

## About the Model

You must have an initial model version in your app bundle. We highly recommend using CoreML (.mlmodel),
but other formats are possible. [See some of our example apps delivering non-CoreML models](https://github.com/skafos/example-ml-apps).

## Setup Silent Background Updates

Note: The following shows how to setup your iOS application for backgroun model updates. Checkout [this guide](sections/push_notifications.md){:target="_blank"} to setup your Skafos app to send models with push notifications. 

### Xcode Setup

In order to receive new models through silent background updates, first we need to enable that functionality in your app.

**Setup Background Modes:**

Select your `workspace` --> `Capabilities` --> `Background Modes`, then:

* turn `on` Background Modes 
* check `Background fetch` and `Remote notifications`

**Setup Push Notifications:**

Select your `workspace` --> `Capabilities` --> `Push Notifications`, then:

* turn `on` Push Notifixations

**Setup Archive Abilitiy:**

Select your `Project` --> `Build Settings`, then:

* Search for `Bitcode`
* Set Enable Bitcode to `no`

### Notification Handler

Now that your app is setup to accept push notifications, embed the `Notification Observer` and `Skafos.reload` method in your view controller and change MyCustomModel() to match your CoreML model name and modelName to match the model name you assigned in the dashboard.

```swift
import UIKit
import Skafos

class MainViewController: UIViewController {
    // This is the model name you assigned on the dashboard
    private let modelName:String = "<your-skafos-model-name>"

    // CoreML automatically uses the name of your .mlmodel file as the class name
    // e.g. MyCustomModel.mlmodel --> MyCustomModel()
    private let myModel = MyCustomModel()

    override func viewDidLoad() {
        super.viewDidLoad()

        // Load a new version of your model if available
        Skafos.load(asset: self.modelName) { (error, asset) in
            // Log the asset in the console
            console.info(asset)
            guard error == nil else {
                console.error("Error: \(String(describing: error))")
                return
            }
            if let model = asset.model {
                // Assign the updated model
                self.myModel.model = model
            }
        }

        /***
        Receive A Notification When A New Model With This Name Has Been Downloaded And Compiled
        ***/
        NotificationCenter.default.addObserver(self, selector:
        #selector(MainViewController.reloadModel(_:)), name:
        Skafos.Notifications.modelUpdateNotification(self.modelName), object: nil)
    }

    /**
    Dynamically updates the ML Model.
    **/
    @objc func reloadModel(_ notification:Notification) {
        // Load a new version of your model if available
        Skafos.load(asset: self.modelName) { (error, asset) in
            // Log the asset in the console
            console.info(asset)
            guard error == nil else {
                console.error("Error: \(String(describing: error))")
                return
            }
            if let model = asset.model {
                // Assign the updated model
                self.myModel.model = model
            }
        }
    }
}
```
