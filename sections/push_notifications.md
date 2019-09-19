# Push Notifications

- Send a silent notification to devices to have them download the latest asset in the background
- Updates can happen behind the scenes and will load the delivered asset to your app the next time you open it.
- Expedite large scale roll out of a particular asset that you'd like your user base to have, over-the-air, without requiring you re-submit the app to the App Store.

### Skafos App Setup

To allow Skafos to send push notifications with your model update, you must upload your push certificates.

First, add your [bundle ID](https://developer.apple.com/documentation/appstoreconnectapi/bundle_ids){:target="_blank"}. This should match the bundle ID used in your iOS application.

<img src="/assets/app_settings_bundle_id.png" width="100%"/>

Then, upload your [push certificate](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_certificate-based_connection_to_apns){:target="_blank"} to the environment(s) you want to receive background model updates.

<img src="/assets/app_settings_push_certs.png" width="100%"/>

[Learn how to setup background update with Skafos](/integrate.md#setup-silent-background-updates){:target="_blank"} in your iOS app.

### Send a Model Update via Push

You can send push notification to all of the devices registered for that app:

- When you are deploying a new model

<img src="/assets/deploy_with_push.png" height="400"/>

- For a model that has already been deployed
  - Warning: Too many consecutive pushes may [throttle your silent notifications](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/sending_notification_requests_to_apns){:target="_blank"}

<img src="/assets/send_push_notification.png" width="400"/>

By default,
- `Prod` push notifications will be default selected to send on Apple's `production` APNS server. 
- `Dev` push notifications will be default selected to send on Apple's `sandbox` APNS server.