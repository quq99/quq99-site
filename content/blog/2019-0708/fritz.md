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



In this post, I would like to share how to deploy tensorflow lite model into android application. This post concentrate more on deployment. For training procedures, refer to [repo](<https://github.com/aobo-y/hair-dye>). And all the android code are available on [repo](<https://github.com/quq99/hair-dye-android>).



# Fritz Androide SDK

Fritz is a platform that allow you to create ML features in your mobile applications with ease. [Fritz repo](<https://github.com/fritzlabs/fritz-repository>)



# Set up Fritz account and initialize the SDK

First we need a Fritz account to upload the model and manage our project. 