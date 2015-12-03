---
layout: post
title: Step by Step - How to create a c++ library with NDK on Android Studio 1.5 (not experimental way)
---

#1. Configure JDK, NDK path environments

####I'm using jdk 1.8.0_65 and ndk-bundle. We can use the official ndk also.

![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554158/d386dbfc-99d8-11e5-863a-c065f5ef11ec.png)



#2. Add javah, ndk-build as External Tools

####(Menu Location is 'Settings > Tools > External Tools')

###2-1. Configure javah
![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554288/187169ac-99da-11e5-92ff-09b78db2a8c6.png)

###2-2. Configure ndk-build
![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554437/63c12cb6-99db-11e5-8cca-cc5875d8e4ef.png)

###2-3. Configure ndk-build clean
![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554470/91964162-99db-11e5-8e20-1cab1825b59b.png)



#3. Create a new Android Studio Project

![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554002/69be1efc-99d7-11e5-990e-a11254ae929e.png)



#4. Add a java class for JNI

![Let's see!](https://cloud.githubusercontent.com/assets/16010352/11554558/632e52be-99dc-11e5-9680-208c35c8bb06.png)



#5. Create a folder for JNI

![screenshot from 2015-12-03 15_36_30](https://cloud.githubusercontent.com/assets/16010352/11554611/f6952154-99dc-11e5-8f82-97cd746f6c1c.png)



#6. Configure build.gradle
####
```javascript
android {
  ...
  defaultConfig {
    ...
    ndk {
      moduleName "your dllname"
    }
    
    sourceSets.main {
      jni.srcDirs = []
      jniLibs.srcDir "src/main/libs"
    }
    ...
  }
  ...
}
```
    
