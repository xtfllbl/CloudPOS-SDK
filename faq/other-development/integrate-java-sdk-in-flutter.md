# Integrate Java SDK in Flutter

### Overview

This guide explains how to add an Android Archive (AAR) file to your Flutter app, enabling you to use native Android functionalities, like a printer API, within your Flutter project.

### Demo Application

To see a practical implementation, download our sample Flutter app that integrates an AAR file and demonstrates how to call a printer API. Download the [flutter demo](https://github.com/SmartPOSSamples/flutterdemo)

### FAQ

* dlopen failed: library "libflutter.so" not found

Please refer to this, [https://github.com/flutter/flutter/issues/29710](https://github.com/flutter/flutter/issues/29710)

Generally two solutions for this issue:

1. Add the follow code to the setting.gradle file

```xml
// 
gradle.beforeProject({ project->
    if (project.hasProperty("target-platform") && !project.getProperty("target-platform").split(",").contains("android-arm")) {
        project.setProperty("target-platform", "android-arm")
    }
})
```

2. Pack for v7a only

```xml
// 
 ndk{
    abiFilters "armeabi-v7a" 
 }
```
