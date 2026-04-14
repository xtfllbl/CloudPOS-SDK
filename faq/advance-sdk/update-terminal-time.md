# Update Terminal Time

### Automatic Update via Wi-Fi

* When the Wi-Fi connection is enabled, the date and time will automatically update.

### Manual Update

* Go to: Settings > Date & Time.
* Disable "Automatic time zone" and "Automatic date & time".
* Manually set the date and time as needed.

### Update via API

* Utilize the Android system clock method to change the system time programmatically.

### Required Permissions

* To use the API method, include the following permission in your application's manifest: **'android.permission.CLOUDPOS\_SETTIME**'.

### Accessing Demo Source

* To understand the implementation details, please download the [complete project demo](https://github.com/SmartPOSSamples/SetTimeDemo).

{% code overflow="wrap" lineNumbers="true" %}
```java
public static void setDateTime(int year, int month, int day, int hour, int minute) throws IOException, InterruptedException {

        Calendar c = Calendar.getInstance();
        c.set(Calendar.YEAR, year);
        c.set(Calendar.MONTH, month-1);
        c.set(Calendar.DAY_OF_MONTH, day);
        c.set(Calendar.HOUR_OF_DAY, hour);
        c.set(Calendar.MINUTE, minute);

        long when = c.getTimeInMillis();
        if (when / 1000 < Integer.MAX_VALUE) {
            SystemClock.setCurrentTimeMillis(when);
        }
        long now = Calendar.getInstance().getTimeInMillis();
        //Log.d(TAG, "set tm="+when + ", now tm="+now);

        if(now - when > 1000)
            throw new IOException("failed to set Date.");

    }
```
{% endcode %}
