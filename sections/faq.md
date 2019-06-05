# Frequently Asked Questions

### **1. I'm getting a "Module Does Not Exist" error in Xcode after installing the Skafos iOS Framework..**
Make sure you've followed the integration guide, using either `CocoaPods` or
`Carthage` as your dependency manager. After you've run the install commands in
your terminal, open up a fresh project workspace and clean house (`cmd + k`, `cmd + shift + k`).

Sometimes you get the `Module Does Not Exist` error if you haven't done a
project build for the first time. Try building and see if the error persists (if you
installed the framework correctly you shouldn't see it anymore).

### **2. Where do I generate an API Token?**
You can generate and revoke API tokens for your account under the
[Account Settings](https://dashboard.skafos.ai/settings/account) page of the dashboard.

### **3. My model is not updating after I deployed with Skafos...**
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

### **4. I cloned an example app and am getting some errors...**
- Do you have Cocoapods or Carthage installed?
- Did you run the install command (`pod install` or `carthage install`)?
- Did you open your workspace (`.xcworkspace`)?
- Did you set your own bundle ID?
- Did you change the team and details in the "Signing" section of "Project -> General"?
- Did you add your Skafos environment keys in the App Delegate?
