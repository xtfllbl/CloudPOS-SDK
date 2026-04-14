# New Android Studio Versions

{% hint style="warning" %}
Newer Android Studio users may need to use updated versions for Android Gradle Plugin (AGP) and Gradle.
{% endhint %}

## How to Change AGP and Gradle Versions

You can change the AGP version in the **build.gradle** file (buildscript —> dependencies —> classpath) by replacing with the current version number. Then, change the Gradle version under Project Structure.&#x20;

The current minimum supported version is **8.6** for Android Studio Jellyfish | 2023.3.1 with AGP **8.4.1**.&#x20;

```gradle
classpath "com.android.tools.build:gradle:8.4.1"
```

## Common Errors

{% hint style="danger" %}
After syncing and building, you may run into other errors.&#x20;
{% endhint %}

### Namespace Missing

Namespace is required for [AGP 8.0.0](https://developer.android.com/build/releases/past-releases/agp-8-0-0-release-notes). If the namespace is missing, it can be added under android in the **build.gradle** file for Module: app. Simply type namespace followed by the same string used by the applicationId under defaultConfig. This is also the same as the package name in the **AndroidManifest.xml** file under manifests. If the applicationId differs from the package name, use the package name.

```gradle
namespace "com.wizarpos.xxx”
```

Some demos may not have an app folder, or the app folder is empty. This is due to the demo being converted from eclipse. In these cases, the two build.gradle files are combined into one file. Similarly, add the namespace under android in the **build.gradle** file, but it should be for Project: name instead of Module: app.

### Package Does Not Exist (aidl files not found)

If the demo uses aidl, add the following lines of code within android {} (also in **build.gradle**) as some new versions have [default value false](https://developer.android.com/build/releases/past-releases/agp-8-0-0-release-notes):

```gradle
buildFeatures {
    aidl(true) 
}
```

### Constant Expression Required <a href="#undefined" id="undefined"></a>

If the demo uses buttons with a switch-case function, you may get an error message "constant expression required" for a line such as case R.id.example. This is due to AGP 8.0.0 having default resources that are [no longer declared final](https://developer.android.com/build/optimize-your-build#use-non-constant-r-classes) for optimized build speed.

You can add android.nonFinalResIds=false to **gradle.properties** or change the switch-case function to if-else statements in the file where the error occurs (generally **MainActivity.java**).

**gradle.properties**

Simply copy the following line to the bottom of the file.

```properties
android.nonFinalResIds=false
```

**Replacement with if-else**

Mouse over the switch keyword and Android Studio should give you the option to replace. Alternatively, Ctrl + 1 or Alt + Enter will also bring up the option. The edited function should look like this:

```java
public void onClick(View v) {
    if (v.getId() == R.id.example) {
        ...
    } else if (v.getId() == R.id.example2) {
        ...
    }
} 
```

### Cannot Find Symbol for AndroidX

Copy the following line under dependencies in **build.gradle**.

```gradle
implementation 'androidx.appcompat:appcompat:1.4.1'
```

You can also manually change the import statements following [this mapping](https://developer.android.com/jetpack/androidx/migrate/class-mappings). For example:

```gradle
//import androidx.annotation.Nullable; becomes
import android.support.annotation.Nullable;
```

Alternatively, you can copy these statements below into **gradle.properties**, but following the mapping is recommended as the [enableJetifier](https://developer.android.com/jetpack/androidx/migrate#migrate_an_existing_project_using_android_studio) flag can lead to slower build times.

```properties
android.useAndroidX=true
android.enableJetifier=true
```

### Could not find method compile()

Some configurations have been deprecated since [Gradle 4.10](https://docs.gradle.org/4.10/userguide/java_plugin.html#sec:java_plugin_and_dependency_management) and removed since [Gradle 7.0](https://docs.gradle.org/7.0/userguide/java_library_plugin.html#sec:java_library_configurations_graph). These include compile, runtime, testCompile, and testRuntime and should be replaced with implementation, runtimeOnly, testImplementation, and testRuntimeOnly respectively in the **build.gradle** file.&#x20;

```gradle
dependencies {
    //compile 'com.android...' replaced with
    implementation 'com.android...'
}
```

### Manifest merger failed

If you receive the following error:

Manifest merger failed : android:exported needs to be explicitly specified for element \<activity#example element>. Apps targeting Android 12 and higher are required to specify an explicit value for android:exported when the corresponding component has an intent filter defined. See [https://developer.android.com/guide/topics/manifest/activity-element#exported](https://developer.android.com/guide/topics/manifest/activity-element#exported) for details.

In the **AndroidManifest.xml** file, copy the following line into the activity element where the error occurs.

```xml
android:exported="true"
```

An example **AndroidManifest.xml** file is below.

```xml
<application
    ...>
    <activity android:name=".MainActivity" android:exported="true">
        <!-- modified line above -->
        ...
    </activity>
</application>
```

## Example build.gradle Files

{% hint style="info" %}
After applying the changes above, your files should look similar to these examples.
{% endhint %}

### build.gradle (Project: Name)

```gradle
buildscript {
    repositories {
        ...
    }
    dependencies {
        classpath "com.android.tools.build:gradle:8.4.1" //change plugin version
    }
}

allprojects {
    repositories {
        ...
    }
}

task clean(type: Delete) {
    ...
}
```

### build.gradle (Module: app)

```gradle
plugins {
    ...
}

android {
    namespace "com.myexample.myapplication" //add namespace
    ...
    defaultConfig {
        applicationId "com.myexample.myapplication"
        ...
    }
    
    buildFeatures { //add if necessary for aidl
        aidl(true)
    }
    ...
}

dependencies {
    implementation 'com.android...' //change compile
    runtimeOnly ... //change runtime
    testImplementation ... //change testCompile
    testRuntimeOnly ... //change testRuntime
    implementation 'androidx.appcompat:appcompat:1.4.1' //add if necessary for androidx
    ...
}
```

### gradle.properties

```properties
...
android.nonFinalResIds=false //add if necessary for case R.id
android.useAndroidX=true
android.enableJetifier=true //not recommended
```
