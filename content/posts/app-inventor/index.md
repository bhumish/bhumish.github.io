---
title: "Android App Inventor Hosting Project"
date: 2012-01-26
draft: false
tags: ["android", "app-inventor", "google", "mit", "hosting", "development"]
categories: ["technology", "projects", "android"]
description: "Hosting Android App Inventor service after Google discontinued support - providing compilation, development and storage services for Android app development"
---

Do you know about the [Android App Inventor](http://en.wikipedia.org/wiki/Google_App_Inventor) service by Google? (Yes, it was developed by Google, but they took back the support last month, and is now in the hands of Massachusetts Institute of Technology.) It allows anyone, including people unfamiliar with computer programming, to create software applications for the [Android operating system](http://en.wikipedia.org/wiki/Android_%28operating_system%29) (OS). It uses a graphical interface, very similar to [Scratch](http://en.wikipedia.org/wiki/Scratch_%28programming_language%29) and the [StarLogo TNG](http://en.wikipedia.org/wiki/StarLogo_TNG) user interface, that allows users to drag-and-drop visual objects to create an application that can run on the Android system, which runs on many mobile devices.

When Google terminated their support to the service, MIT offered their services to support the application development. MIT had asked individuals to host the service on their machines by providing scripts for the compiling of the apps. I was among the volunteers to host the service and provide my space for the compiling, developing and storing their apps.

I developed a Linux RHEL 5 server, configured the services for application development – File Transfer Protocol, Domain Name System, HTTP Transfer and Port Mapping; and also connected the machine with Google AppEngine to run the scripts on my machine while developing the apps and testing through the emulator. Last week I hosted the service for a selected group on trail basis, and the service is working fine. So now I am announcing it open for you all to test my service – develop Android apps the easiest way – store/download your apps – build the apk for your app – or just play with your apps on the emulator. Feel free to develop-test the apps your way – and to report problems, if any, through email.

You can find my App Inventor Server at : [http://androinventor.appspot.com](http://androinventor.appspot.com)