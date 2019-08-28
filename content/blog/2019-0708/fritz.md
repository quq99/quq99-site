---
date: "2019-08-17T20:14:59+08:00"
publishdate: "2019-08-17+08:00"
lastmod: "2019-08-17+08:00"
draft: false
title: "Deploy the hair segmentation model to android application"
tags: ["machine_learning", "blog", "android", "tensorflow"]
series: ["my_machine_learning_journey"]
categories: ["Tools"]
img: "images/blog/series/my_machine_learning_journey/2019-08/cover2.png"
toc: true
summary: "This post shows how to deploy tensorflow lite model into android application"
---



In this post, I would like to share how to deploy tensorflow lite model into android application. This post concentrate more on deployment. For training procedures, refer to [repo](<https://github.com/aobo-y/hair-dye>). And all the android code is available on [repo](<https://github.com/quq99/hair-dye-android>).



# Fritz Androide SDK

Fritz is a platform that allow you to create ML features in your mobile applications with ease. [Fritz repo](<https://github.com/fritzlabs/fritz-repository>)



# Set up Fritz account and initialize the SDK

First we need a Fritz account to upload the model and manage our project. Sign up a Fritz account and create a project. Then add an android application. Follow the instructions:

## Register your app

Follow the instructions provided by Fritz.

## Add the Fritz SDK

* Install Fritz Core via Gradle

  1. In your root-level Gradle file (`build.gradle`), include the Maven repository for Fritz.

  

  ```json
  allprojects {
      repositories {
          maven { url "https://raw.github.com/fritzlabs/fritz-repository/master" }
      }
  }
  ```

  2. In your app-level Gradle file (`app/build.gradle`), add the dependency for the core SDK.

  

  ```json
  dependencies {
      implementation 'ai.fritz:core:3+'
  }
  ```

## Edit your AndroidManifest.xml

* Register the FritzCustomModelService in your AndroidManifest.

  

  ```php+HTML
  <manifest xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- For model performance tracking & analytics -->
      <uses-permission android:name="android.permission.INTERNET" />
  
      <application>
          <!-- Register the custom model service for OTA model updates -->
          <service
              android:name="ai.fritz.core.FritzCustomModelService"
              android:exported="true"
              android:permission="android.permission.BIND_JOB_SERVICE" />
      </application>
  </manifest>
  ```

## Initialize Fritz

* Before managing custom models or using Fritz features, initialize the SDK by calling **Fritz.configure()** with your API Key. This only needs to be done once when the app launches.

  Add the following code into MainActivity class. The API key can be seen on dashboard "Project Settings -> Project Apps -> Actions -> show API key".

  ```java
  public class MainActivity extends AppCompatActivity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          // Initialize Fritz
          Fritz.configure(this, "API key");
      }
  }
  ```



# Add the HairNet model

## upload the tensorflow lite model

Click the ...



## Add Fritz’s TFLite Library

In your app-level Gradle file (`app/build.gradle`),

```json
dependencies {
    implementation 'ai.fritz:core:3+'
    implementation "ai.fritz:vision:3+"
    implementation 'ai.fritz:custom-model-tflite:3+'
}
```

This can make you include your own tensorflow model into your application.



## no compress model when build the apk

Under the hood, we use [TensorFlow Lite](https://heartbeat.fritz.ai/how-tensorflow-lite-optimizes-neural-networks-for-mobile-machine-learning-e6ffa7f8ee12) as our mobile machine learning framework. In order to make sure that the model isn’t compressed when the APK is built, you’ll need to add the following in the same build file under the `android` option.

```json
android {
	aaptOptions {
        noCompress "tflite"
        noCompress "lite"
    }
}
```





# Create a Segmentation Predictor with a Hair Segmentation model

We can either include your model with the app or load the model when the app runs (recommended to reduce the size of your APK). In my project, I include my model on device.

## Create model class

In Dashboard, Click "Custom Models" and choose your uploaded model, click and then click "SDK Instructions". You can see a brief instruction. And our model ID so that he Fritz can monitor the model's performance. Because we include the model on device rather than load the model at running time. I placed the model on local. The model is placed in `/app/src/main/assets/converted_model_hairnet.tflite`.

Also, I found that the instructions provided by Fritz did not work well for me. So, I search the documentation and create my own model class.

...



##  Set up a predictor using own model

in setupPredictor() method in MainActivity class

```java
SegmentOnDeviceModel onDeviceModel = new Train_170CustomModel();
predictor = FritzVision.ImageSegmentation.getPredictorTFL(onDeviceModel);

```



# Choose a hair color for prediction



# Run prediction on an image to detect hair



# Blend the mask onto the original image





# Track the performance of your model

