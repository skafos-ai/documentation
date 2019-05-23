[<img src="images/skafos_mark.png" width=10%>](https://skafos.ai)


# Welcome to Skafos!

Skafos is the tool for deploying machine learning models to mobile apps and managing the same models in a production environment. Built to integrate with any of the major cloud providers, users can utilize AWS, Azure, Google, IBM or nearly any other computational environment to organize data and train models. Skafos then versions, manages, deploys, and monitors model versions running in your production application environments. A recommended functional architecture looks something like this:

[Diagram] 
DATA — TRAINING ENV (python SDK) — SKAFOS — (iOS Framework) PHONES

Skafos is internally structured to support organizations (or individuals) who develop apps with machine learning models that power the next generation of mobile experiences. Given that most production mobile applications are supported by small to medium-sized teams, Skafos requires the creation of an organization from which to manage a team of one or more users. For any given organization, Skafos has the following hierarchical structure:

[Diagram] APPS -- MODELS -- MODEL VERSIONS

## Applications

Skafos applications represent an iOS application integration. Create a new Skafos application for each new iOS app with a unique bundle ID. Utilize application environments to manage development and production releases. 

* Manage your Skafos application name and application environments. 
* Environment keys are managed at the application level.

## Models
Skafos models represent a component of your application powered by a machine learning artifact. Models are a collection of model versions, and environments to which model versions are deployed. Create a new Skafos model for each discrete ML-powered feature. 

* Manage your Skafos model name, and model version deployments here.


## Model Versions
Skafos model versions are deployable machine learning artifacts such as Core ML and TensorFlow Lite files. Model versions are automatically version-controlled by Skafos when saved, can be loaded into remote training environments for evaluation or retraining, and can be deployed to mobile devices for on-device inference. 

* Model versions may be assigned to environments.
* Model versions are zipped archives. Skafos compresses on your behalf in the python SDK. If you use the dashboard, you are required to zip your files prior to upload. 


## Python SDK and iOS Framework
To successfully integrate Skafos into your existing apps and Machine Learning model training environment, use the Skafos Python SDK and iOS Framework. 
 
* [Python SDK](https://pypi.org/project/skafos/)
* iOS Framework

## Have questions? Need help?
Join our Slack Community! Click the icon below for a link.

[<img src="images/Slack_Mark_Web.png" width=15%>](https://skafosai.slack.com/join/shared_invite/enQtNTAxMzEwOTk2NzA5LThjMmMyY2JkNTkwNDQ1YjgyYjFiY2MyMjRkMzYyM2E4MjUxNTJmYmQyODVhZWM2MjQwMjE5ZGM1Y2YwN2M5ODI)
