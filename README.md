# CrosswalkDemo
A simple project showing how to embed Crosswalk into an Android application.

*Note*: The Crosswalk team has stopped development on this project.  You can read more about it here: [Crosswalk 23 to be the last Crosswalk release](https://crosswalk-project.org/blog/crosswalk-final-release.html)

# Setup
To open this project in Android Studo:

1. Download the project or use git to sync it to your computer.
2. In Android Studio choose: File > Import Project ...
3. Navigate to your project on disk, select it and choose "OK".

# Run
You can run the project in Android Studio or create an APK with the following command:


`./gradlew assembleRelease`

or

`./gradlew assembleDebug`

# Exclude x86 libraries
If you want to exclude x86 libraries for a smaller APK, then uncomment this code in build.gradle.  This will only build armeabi-v7a libraries.

```
// Remove other libraries
ndk {
    abiFilters "armeabi-v7a"
}
```

# 64 Bit Build
Crosswalk creates the binaries for ARM 64 here: [https://download.01.org/crosswalk/releases/crosswalk/android/maven2/org/xwalk/xwalk_core_library/20.50.533.12](https://download.01.org/crosswalk/releases/crosswalk/android/maven2/org/xwalk/xwalk_core_library/20.50.533.12)

To use one of these instead, first you need to download it:
```
curl -O https://download.01.org/crosswalk/releases/crosswalk/android/maven2/org/xwalk/xwalk_core_library/20.50.533.12/xwalk_core_library-20.50.533.12-arm64.aar
```

Then install it to your local maven repository:

```
mvn install:install-file -DgroupId=org.xwalk -DartifactId=xwalk_core_library \
      -Dversion=20.50.533.12-arm64 -Dpackaging=aar  \
      -Dfile=xwalk_core_library-20.50.533.12-arm64.aar \
      -DgeneratePom=true
```

Update your build.gradle to use your local maven repository:
```
repositories {
    mavenLocal()
}
```

Then you can reference it in your build.gradle:
```	  
compile 'org.xwalk:xwalk_core_library:20.50.533.12-arm64'
```


https://crosswalk-project.org/blog/using-custom-crosswalk-in-cordova-plugin.html

More details here: [https://diego.org/2015/01/07/embedding-crosswalk-in-android-studio/](https://diego.org/2015/01/07/embedding-crosswalk-in-android-studio/)

# Links
* Blog post with more details here: [https://diego.org/2015/01/07/embedding-crosswalk-in-android-studio/](https://diego.org/2015/01/07/embedding-crosswalk-in-android-studio/)
* [Crosswalk Downloads](https://crosswalk-project.org/documentation/downloads.html)
* [How to change the Crosswalk version used by the Cordova Crosswalk Webview plugin](https://crosswalk-project.org/blog/using-custom-crosswalk-in-cordova-plugin.html)
