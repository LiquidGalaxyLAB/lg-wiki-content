---
title: How to rebuild apks from older flutter files
contributor: Tathagat Kumar
date: March 1, 2025
---
## Overview
# How to rebuild apks from older flutter files #
---
Many times, we have an urgent need to compile an apk of a flutter file that we made in the past only to find bugs and errors while rebuilding the apk in the future again. Such errors arise due to several reasons such as deprecated packages, compatibility issues etc. The below documentation will guide on how to tackle the possible errors you will encounter while rebuilding apk of an old flutter app

1. Verifying your current flutter SDK: 
Using the right flutter SDK is necessary sometimes in order to adjust to the needs of the flutter file that we are trying to rebuild. For ex: From flutter 3.10.0, dart 3 was introduced.This upgrade to Dart can introduce incompatibilities if the project was written for a version prior to Dart 3. It's important to ensure the Flutter SDK you're using matches the Dart version expected by your project.

You may verify your flutter version by the following command
~~~bash
Flutter --version 
~~~

If you wish to switch your flutter version, you may either do it manually with the help of environmental variables or you may use a FVM (Flutter version manager) as follows:

First, install FVM as follows:
~~~bash
dart pub global activate fvm
~~~
Now, to install a specific Flutter version, use:
~~~bash
fvm install <version>
~~~
To switch to your desired version:
~~~bash
fvm use <version>
~~~

2. Migrate the flutter project:
 Since our project is built in an older version of Flutter, run “flutter pub get” to fetch the 
dependencies.
In the process, look out for the deprecated or breaking changes in the code which occurs due to                                             
 many flutter packages migrating and release a totally new version of that package, abandoning the   
 old packages and their support completely.
 In such cases, I recommend mending the code according to the new flutter package that is in 
 support and use. 
 In several cases, I find sticking to older versions of flutter package that have support is better than 
 migrating to newer versions of flutter packages sometimes. Here, just try to update your 
 dependencies in your pubspec.yaml file and experiment out the way that works for you.

3. Ensure android-specific configuration: 
One of the most important things you might to keep in mind while rebuilding an apk would be this one. 


Update Gradle:
Navigate to the `android/ directory` and open `build.gradle`.
Ensure Gradle wrapper and Android Gradle plugin versions are up-to-date.
Set Compile SDK Version:
Ensure your `android/app/build.gradle` specifies a valid `compileSdkVersion` and `targetSdkVersion`.
~~~dart
android {
  compileSdkVersion 33
  defaultConfig {
	targetSdkVersion 33
  }
}
~~~

4. Testing the APK: 
Now after successfully making changes and migrating your old flutter project, it’s time to test it out. It is mostly advisable to run the app in debug mode first and then in release mode, as such a practice helps you to troubleshoot any error you might encounter otherwise.

