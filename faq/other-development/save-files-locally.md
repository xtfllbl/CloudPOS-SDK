# Save Files Locally

### Android Storage Permissions Explanation

For Android SDK below 30, directly request the following permissions in AndroidManifest.xml:

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

For Android SDK above 30, the following permissions need to be requested:

{% code overflow="wrap" %}
```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.MANAGE_EXTERNAL_STORAGE"/>(New in Android 11 and above)
```
{% endcode %}

If only the following read and write storage permissions are requested on Android 11 and above: android.permission.READ\_EXTERNAL\_STORAGE and android.permission.WRITE\_EXTERNAL\_STORAGE, it only allows access to public storage, such as Downloads/, Documents/, etc., and does not allow operations on the terminal's file management. If you need access to all files in the shared storage space, you need to request android.permission.MANAGE\_EXTERNAL\_STORAGE.

#### Save to a Public Directory

If you want to save public files on the external storage, use the getExternalStoragePublicDirectory() method to get a File representing the appropriate directory on the external storage. The method takes an argument specifying the type of file you want to save so that they can be logically organized with other public files, such as DIRECTORY\_MUSIC or DIRECTORY\_PICTURES. For example:

{% code overflow="wrap" lineNumbers="true" %}
```java
public File getPublicAlbumStorageDir(String albumName) {
    // Get the directory for the user's public pictures directory.
    File file = new File(Environment.getExternalStoragePublicDirectory(
            Environment.DIRECTORY_PICTURES), albumName);
    if (!file.mkdirs()) {
        Log.e(LOG_TAG, "Directory not created");
    }
    return file;
}
```
{% endcode %}

#### Save to a Private Directory

If you want to save files on external storage that are private to your app and not accessible by the MediaStore content provider, you can acquire a directory that's used by only your app by calling getExternalFilesDir() and passing it a name indicating the type of directory you'd like. Each directory created this way is added to a parent directory that encapsulates all your app's external storage files, which the system deletes when the user uninstalls your app.

_Caution:_ Files on external storage are not always accessible, because users can mount the external storage to a computer for use as a storage device. So if you need to store files that are critical to your app's functionality, you should instead store them on internal storage.

For example, here's a method you can use to create a directory for an individual photo album:

{% code overflow="wrap" lineNumbers="true" %}
```java
public File getPrivateAlbumStorageDir(Context context, String albumName) {
    // Get the directory for the app's private pictures directory.
    File file = new File(context.getExternalFilesDir(
            Environment.DIRECTORY_PICTURES), albumName);
    if (!file.mkdirs()) {
        Log.e(LOG_TAG, "Directory not created");
    }
    return file;
}
```
{% endcode %}

If none of the pre-defined sub-directory names suit your files, you can instead call getExternalFilesDir() and pass null. This returns the root directory for your app's private directory on the external storage.

Remember that getExternalFilesDir() creates a directory that is deleted when the user uninstalls your app. If the files you're saving should remain available after the user uninstalls your app—such as when your app captures photos and the user should keep those photos—you should instead save the files to a public directory.

Regardless of whether you use getExternalStoragePublicDirectory() for files that are shared or getExternalFilesDir() for files that are private to your app, it's important that you use directory names provided by API constants like DIRECTORY\_PICTURES. These directory names ensure that the files are treated properly by the system. For instance, files saved in DIRECTORY\_RINGTONES are categorized by the system media scanner as ringtones instead of music.

#### Select Between Multiple Storage Locations

Sometimes, a device that allocates a partition of the internal memory for use as the external storage also provides an SD card slot. This means that the device has two different external storage directories, so you need to select which one to use when writing "private" files to the external storage.

Beginning with Android 4.4 (API level 19), you can access both locations by calling getExternalFilesDirs(), which returns a File array with entries for each storage location. The first entry in the array is considered the primary external storage, and you should use that location unless it's full or unavailable.

If your app supports Android 4.3 and lower, you should use the support library's static method, ContextCompat.getExternalFilesDirs(). This always returns a File array, but if the device is running Android 4.3 and lower, then it contains just one entry for the primary external storage (if there's a second storage location, you cannot access it on Android 4.3 and lower).

getExternalFilesDirs(): This method takes a String argument, type, which specifies the type of files directory to return. For example, Environment.DIRECTORY\_PICTURES can be used if you are interested in the directory for storing pictures. If type is null, it returns the root of the files directory.

The method returns an array of File objects, one for each external storage device. The first entry in the array is the same as the file returned by getExternalFilesDir(String), which is the primary external storage. Additional entries in the array represent any additional mounted external storage devices, such as SD cards or USB drives.

Access to the external storage requires appropriate permissions. Before API level 19 (Android 4.4 KitKat), read and write permissions are needed. Starting from API level 19, only read permission is required to read from external storage, and no permissions are required to write to external storage in the directories returned by this method.

\<uses-permission android:name="android.permission.READ\_EXTERNAL\_STORAGE" />

{% code overflow="wrap" lineNumbers="true" %}
```java
 
public class MyActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my);

        // Get all available external file directories (including SD card paths)
        File[] externalFilesDirs = getExternalFilesDirs(null);

        for (File file : externalFilesDirs) {
            // Process each path as needed
            Log.d("ExternalFilesDir", "Path: " + file.getAbsolutePath());
        }
    }
}
```
{% endcode %}

PS.getExternalStoragePublicDirectory()/ getExternalFilesDir(), the return of these method is the primary external storage(/storage/emulated/0/).

_See Also:_ [Data and file storage overview](https://developer.android.com/training/data-storage/files#WriteExternalStorage) from developer.android.com.

