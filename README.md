# KobitonCircleCI

This project coordinates the Appium tests workflow. These workflows run nightly, from Monday to Friday.

In the [config file](https://github.com/freeletics/KobitonCircleCI/blob/master/.circleci/config.yml), you will find two workflows: one for Android and one for iOS. In each of them, the following steps happen:

### 1. Data Creation

It calls the job postman_test_data to create the testing data. In this job, Postman Data generator is called to create users in the Integration environment.

The specific Postman collections used for this step are the following:
https://github.com/freeletics/postman-data-generator/tree/master/appium_data

### 2. Build mobile clients

It calls the respective jobs to generate the testing builds for Android and iOS. 
- For Android, it's a release client build 
- For iOS, it's an Alpha client build 
Both build are set to the environment Integration. 

### 3. Upload the testing builds and Run the tests

In this step, we call the jobs run_appium_tests_android and run_appium_tests_ios.

In these jobs, we call Kobiton's APIs to delete the current app and upload the new version. Then we run the command to trigger the tests. The specific API calls are documented with comments in the code.

### 4. Cleanup

After the tests run, we need to delete claims (subscriptions) and the users. To do that, we again use Postman Data Generator. 

This step will not run if the test execution has failed.

# Appium tests

ℹ️ To learn more about how Appium works at Freeletics, please check its repository: https://github.com/freeletics/Appium_e2e_tests


# Architecture

### Integrating Kobiton into CircleCI mobile application development pipeline

In mobile application development, performing testing on **real** devices before releasing is a crucial, but also costly process, which means that only few developers are able to perform testing on real devices, but only a very limited range of devices.

By integrating Kobiton into your mobile application development pipeline, CircleCI will be able to execute an automation testing on real devices, which help improve development process and product quality.

This guide is applicable if you are using these tools and technologies in your pipeline:
- ReactNative as a technology to develop the mobile application.
- Appium as a framework to develop the automation test scripts.
- CircleCI as a CI/CD tool.
- GitHub as a VCS provider to store your test scripts on.

<img src="docs/assets/diagram.svg"/>

Refer to [our documentation](./docs/README.md) for more details on how to integrate Kobiton with CircleCI.
