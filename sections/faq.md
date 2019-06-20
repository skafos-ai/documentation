# Frequently Asked Questions

## Xcode & iOS Related
### **1. I'm getting a "Module Does Not Exist" error in Xcode after installing the Skafos iOS Framework..**
Make sure you've followed the integration guide, using either `CocoaPods` or
`Carthage` as your dependency manager. After you've run the install commands in
your terminal, open up a fresh project workspace and clean house (`cmd + k`, `cmd + shift + k`).

Sometimes you get the `Module Does Not Exist` error if you haven't done a
project build for the first time. Try building and see if the error persists (if you
installed the framework correctly you shouldn't see it anymore).

### **2. I cloned an example app and am getting some errors...**
- Do you have Cocoapods or Carthage installed?
- Did you run the install command (`pod install` or `carthage install`)?
- Did you open your workspace (`.xcworkspace`)?
- Did you set your own bundle ID?
- Did you change the team and details in the "Signing" section of "Project -> General"?
- Did you add your Skafos environment keys in the App Delegate?

### **3. There are errors in the console related to ATS Security Protocol...**
Sometimes you might see errors like this:
```
2019-05-20 13:09:23 App Transport Security has blocked a cleartext HTTP (http://) resource load since it is insecure. Temporary exceptions can be configured via your app's Info.plist file.
2019-05-20 13:09:23 Cannot start load of Task <B05C79B0-571D-4629-BA8D-490013343849>.<1> since it does not conform to ATS policy.
```

Fortunately it's an easy fix. Just add this setting to your app's `Info.plist` file:
```
<key>NSAppTransportSecurity</key>
<dict>
  <key>NSAllowsArbitraryLoads</key>
  <true/>
</dict>
```
Use a text editor like Vim and insert the above snippet within the `<plist>..</plist>` component.


## Skafos Workflow Related
### **1. Where do I generate an API Token?**
You can generate and revoke API tokens for your account under the
[Account Settings](https://dashboard.skafos.ai/settings/account) page of the dashboard.

### **2. My model is not updating after I deployed with Skafos...**
There are a couple things to check to make sure you see the model update after a
deployment:
- Was the model deployed to the right environment?
- Did you trigger a call to the `Skafos.load` function?
- How big is your model? Large models may take some time to download in the app
depending on network speed and bandwidth.
- Are you watching the console area debug logs?
- Are you setting the right `modelName` variable? Should be the same name used in the Skafos dashboard.

If you've check each of these things and are still having trouble, [reach out to
us on Slack](https://skafosai.slack.com/join/shared_invite/enQtNTAxMzEwOTk2NzA5LThjMmMyY2JkNTkwNDQ1YjgyYjFiY2MyMjRkMzYyM2E4MjUxNTJmYmQyODVhZWM2MjQwMjE5ZGM1Y2YwN2M5ODI)
and we will provide assistance.

### **3. Can I use a non-CoreML artifact as my machine learning model?**
Yes. Apple built CoreML to play nicely in Swift and Xcode. Skafos integrates with CoreML seamlessly (see all of our example apps). However, Skafos can be used to deploy arbitrary files. So if you are trying to deploy another model format like
TensorFlow Lite or DLib, there's nothing stopping you.

Check out this example app where Skafos delivers and integrates a non-CoreML
model.

### **4. Does Skafos handle model training?**
Skafos does not handle model training directly. Because each ML app and use-case is unique, Skafos is built to support any training environment you choose. We provide a [Python SDK](https://sdk.skafos.ai) for you to upload models to Skafos from wherever is most convenient for you.
