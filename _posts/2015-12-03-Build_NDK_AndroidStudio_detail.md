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



#7. First Build

####We will encounter an error like 'Error: NDK integration is deprecated in the current plugin. blah blah'.
####Because we are not using the experimental class for NDK.
####Let's add one line in 'gradle.properties'.
####
```javascript
android.useDeprecatedNdk=true
```
####And build again, it must be succeeded.



#8. Create a JNI header file

####Use 'NDK external tools - javah'

![screenshot from 2015-12-03 15_40_32](https://cloud.githubusercontent.com/assets/16010352/11555467/c996de52-99e3-11e5-8a46-cb62d15fc568.png)

####Then we will have a JNI header file.

![screenshot from 2015-12-03 15_41_07](https://cloud.githubusercontent.com/assets/16010352/11555570/970ad000-99e4-11e5-9d1c-0a4b284579ff.png)



#9. Create a C++ source file

####We don't need to check "Create associated header".

![screenshot from 2015-12-03 15_42_13](https://cloud.githubusercontent.com/assets/16010352/11555636/1cd4f634-99e5-11e5-94d2-2dfddd32ce2b.png)

![screenshot from 2015-12-03 15_42_26](https://cloud.githubusercontent.com/assets/16010352/11579130/ad905a36-9a6e-11e5-8e46-2606d76173ec.png)

![screenshot from 2015-12-03 15_43_55](https://cloud.githubusercontent.com/assets/16010352/11555689/7f4df52c-99e5-11e5-8296-e0c2abe95318.png)



#10. Create some MakeFiles

####Android.mk

![screenshot from 2015-12-03 15_44_24](https://cloud.githubusercontent.com/assets/16010352/11579169/eea922aa-9a6e-11e5-9605-f84de8f9f10b.png)

![screenshot from 2015-12-03 15_44_37](https://cloud.githubusercontent.com/assets/16010352/11579200/3cfbb1d4-9a6f-11e5-94cb-77ae693fbc85.png)

![screenshot from 2015-12-03 15_45_44](https://cloud.githubusercontent.com/assets/16010352/11579206/48a66b32-9a6f-11e5-894e-5093d0bc1e4f.png)


####Application.mk

![screenshot from 2015-12-03 15_46_24](https://cloud.githubusercontent.com/assets/16010352/11579219/66d0280a-9a6f-11e5-8a00-066f83bed8cb.png)



#11. Build Our NDK Library

![screenshot from 2015-12-03 15_51_28](https://cloud.githubusercontent.com/assets/16010352/11579229/7dc9efaa-9a6f-11e5-8e37-a1e5e3e8d481.png)

![ndk_build_result](https://cloud.githubusercontent.com/assets/16010352/11579248/bbee21b6-9a6f-11e5-8477-4cc651b16db1.png)


#12. Let's Use Our NDK Library Function

![use_ndk](https://cloud.githubusercontent.com/assets/16010352/11579359/c1d728e2-9a70-11e5-866e-fccba40ada67.png)


#13. Final Build and Create APK

####After build, We must have our library in the APK.

![screenshot from 2015-12-03 15_54_57](https://cloud.githubusercontent.com/assets/16010352/11579393/174adb66-9a71-11e5-852f-201a1edabc58.png)

![screenshot from 2015-12-03 15_55_12](https://cloud.githubusercontent.com/assets/16010352/11579398/224c583c-9a71-11e5-8ae5-50175fb88aab.png)


#14. Let's Enjoy NDK :)

