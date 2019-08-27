<img src="https://docs.skafos.ai/assets/skafos_mark.png"
     width="40" height="40"
     style="float: left; margin-right: 10px; margin-bottom: 20px;" />
<img src="/assets/makeml/plus_sign.png"
      width="20" height="20"
      style="float: left; margin-right: 10px; margin-bottom: 10px;margin-top: 10px;" />
<img src="/assets/makeml/makeml.png"
     width="40" height="40"
     style="float: left; margin-right: 20px; margin-bottom: 20px;" />

##### Creating ML powered mobile app experiences

__

### [MakeML](https://makeml.app/){:target="_blank"} and Skafos: Object Detection App

Here we'll highlight how MakeML and Skafos seamlessly work together to create an ML powered iOS mobile application.

* **MakeML** supports data importing, labeling, formatting, and model training by providing a convenient markup tool for images and a converter for model ready data. Check out their [docs](https://makeml.app/docs/doc1){:tarket="_blank"} on training an Object Detection model.

* **Skafos** supports the integration, delivery, and monitoring of your MakeML model in your iOS application.

The instructions below detail how to use the integration point between MakeML and Skafos.

#### Export your Model from MakeML to Skafos

* Navigate to the trainings window in the MakeML app.
* When your model is finished training, you'll have the option to export your CoreML artifact or deploy to Skafos. Select Deploy to Skafos.ai.

<img src="/assets/makeml/training_window.png"
     height="400"
     style="float: center; margin: 0 auto; display: block;" />

* You will be prompted to enter your Skafos.ai API key. You can find your API tokens in the [account settings page](https://dashboard.skafos.ai/settings/account){:target="_blank"} in the dashboard, as shown below. In MakeML, you can also check the box Remember API Key, so you don't have to enter it each time.

<img src="/assets/api_tokens.png"
     style="float: center; margin: 0 auto; display: block;" />

* Select your organization, the app, and its model. Then, click upload. Your model will be uploaded to Skafos and will be ready for delivery. You should see the deploy buttons become enabled in the MakeML app. 

<img src="/assets/makeml/deploy_model_version.png"
     height="400"
     style="float: center; margin: 0 auto; display: block;" />

* To deliver this newly trained model to your app, click Deploy to Prod or Deploy to Dev. These environment groups are set by your keys in the `AppDelegate.swift` file and determine the environment from which models will be downloaded.
* For more details on the app side, check out our [Integration Guide](../integrate.md){:target="_blank"}.