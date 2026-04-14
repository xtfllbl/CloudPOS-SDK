# Set Wallpaper

### Code Snippet

* Utilize the provided code snippet in your project for setting the wallpaper. Ensure to integrate it correctly within your application's code structure.

{% code overflow="wrap" lineNumbers="true" %}
```xml
<uses-permission android:name = "android.permission.SET_WALLPAPER"/>
```
{% endcode %}

{% code overflow="wrap" lineNumbers="true" %}
```java
public void setWallPaper() {
    WallpaperManager mWallManager = WallpaperManager.getInstance(context);
    try {
        mWallManager.setResource(R.drawable.wallpaperCos);
        mHandler.obtainMessage(2, "set setWallPaper success...").sendToTarget();
    } catch (Exception e) {
        e.printStackTrace();
        mHandler.obtainMessage(3, "set setWallPaper fail...").sendToTarget();
    }
}
```
{% endcode %}

### Demo Project

* Access the complete demo project for a practical example. This demo can serve as a guide to understand the implementation details and context of the wallpaper setting feature.
* Please get the [whole demo](https://github.com/SmartPOSSamples/SetWallpaperDemo.git).

