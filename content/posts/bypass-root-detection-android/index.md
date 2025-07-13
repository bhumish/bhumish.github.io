---
title: "Bypass Root detection in Android - by modifying the APK"
date: 2017-12-16
draft: false
tags: ["android", "security", "root-detection"]
categories: ["Security"]
---

Developers implement root-detection mechanism in Android to prevent users from using their app on a rooted phone. The app (apk) will implement different checks to determine whether the phone is rooted or not. Later, after this check, if the phone is rooted then the APK will display some message like:

- "This device is rooted, exiting the application"
- "This application will not work on rooted device, exiting!"

And it will exit the application.

## The Bypass Strategy

**How to bypass this:**
- **(a)** The APK checks at the device level and determines that the device is rooted
- **(b)** APK will display the message and close the application

Between step **(a)** and step **(b)**, let the APK know that the device is rooted - but before it gives the command to exit the application – we can change the code to **not exit the application** even if the device is rooted.

Below are the technical steps to perform this. This method works most of the times, and doesn't need Xposed modules or other tools.

## Technical Steps

Let's refer the APK/Application as `test.apk` for this article.

### Step 1: Decompile the APK

Decompile the APK by using [apktool](https://ibotpeaches.github.io/Apktool), with the following command:

```bash
apktool d test.apk
```

The code of this apk will be available in a folder named `test`. There will be smali files in the folder, which will have all the application code.

### Step 2: Find the Root Detection Code

Search for text like `rooted`, `exiting` or `root` – according to the message which is being displayed when you start this application on a rooted phone. Note the name of the file which is containing this text, open it in a text editor.

### Step 3: Modify the Logic

Functionality will be like this:

```
APK will check the device is rooted:
if yes (e.g. equals to 0),
    exit
if no (e.g. not equals to 0),
    continue
```

If you make the condition as `not equals to 0`, it will not exit and allow the application to run.

### Step 4: Rebuild the APK

After making this change, re-compile/build the APK by using apktool with following command:

```bash
apktool b test test-new.apk
```

A new apk will be created with the name `test-new.apk`.

### Step 5: Sign the APK

Create a key and sign the apk with following commands:

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore test-new.apk alias_name
```

### Step 6: Install the Modified APK

Now the APK is built, signed and ready for installation. Install this APK by using [ADB](https://developer.android.com/studio/command-line/adb) and now it will allow the application to run on a rooted Android device.

## Summary

This method involves:
1. **Decompiling** the APK to access its source code
2. **Finding** the root detection logic in the smali files
3. **Modifying** the conditional logic to bypass the exit command
4. **Rebuilding** and **signing** the APK
5. **Installing** the modified APK on the rooted device

This approach works for most applications and doesn't require additional tools like Xposed modules, making it a straightforward solution for bypassing root detection mechanisms.