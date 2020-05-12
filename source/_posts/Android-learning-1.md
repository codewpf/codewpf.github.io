---
title: Android learning 1
date: 2020-05-12 22:01:15
categories: Android
tags: 
- Android
- Kotlin
- IntelliJ
---



## First blood - Install Android SDK

### IntelliJ - error
A problem occurred configuring project ':app'.
> The SDK directory '/Users/eleven/Documents/Ktolin/AppDemo/PleaseSpecifyAndroidSdkPathHere' does not exist.


update the `local.properties` file:

```kotlin
sdk.dir=PleaseSpecifyAndroidSdkPathHere

PleaseSpecifyAndroidSdkPathHere -> /Users/*user name*/Library/Android/sdk
```

<!-- more -->


### brew install - fail
* brew update
* brew install android-sdk
> No available formula with the name "android-sdk"
>
> Found a cask named "android-sdk" instead. Try
> 
> brew cask install android-sdk 

* brew cask install android-sdk
> The "android" command is deprecated.
> 
> For manual SDK, AVD, and project management, please use Android Studio.
> 
> For command-line tools, use tools/bin/sdkmanager and tools/bin/avdmanager
>

* brew cask uninstall android-sdk


### install by IntelliJ (macOS) - Done

#### download sdk 

* open IntelliJ
* -> Preferences
* -> Appearance & Behavior
* -> System setting
* -> Android SDK
* -> Android SDK Location: xxx, click `Edit` button
* -> select the check box and click `Next`
* -> download finished

#### configuration

* create project page
* -> Click `configure` button (bottom and right corner)
* -> Structure for New Projects
* -> Change `<No SDK>` to your java version(mine is 1.8)
* -> Check Android SDK is ready in `Platform Settings -> SDKs`




