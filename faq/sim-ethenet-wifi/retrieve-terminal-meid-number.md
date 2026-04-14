# Retrieve Terminal MEID Number

This guide provides instructions on how to retrieve the MEID number of your terminal using a specific code snippet.

#### Code Snippet for MEID Retrieval

To obtain the MEID, use the following code snippet:

* Android version less than 12:

{% code overflow="wrap" lineNumbers="true" %}
```java
  private static String getMEID(Context context,TelephonyManager telephonyManager){
     String meid = null;
     int count = telephonyManager.getPhoneCount();
        for (int i = 0; i < count; i++) {
            int[] subIds = SubscriptionManager.getSubId(i);
            int phoneType = telephonyManager.getCurrentPhoneType(subIds[0]);
            if(phoneType == TelephonyManager.PHONE_TYPE_CDMA){
              meid = telephonyManager.getDeviceId(i);
              android.util.Log.d("meid ", " meid slot"+ i +" = "+ meid);
              break;
            }
        }
        if(!TextUtils.isEmpty(meid)&&(meid.length() == 14 || meid.length() == 15)){
         return meid;
        }
        meid = Settings.Global.getString(
             context.getContentResolver(),"cdma_meid_with_no_card");
        android.util.Log.d("meid ", meid);
        if(!TextUtils.isEmpty(meid)&&(meid.length() == 14 || meid.length() == 15)){
         return meid;
        }
     return "";
    }
```
{% endcode %}

* Android version equal to 12:

{% code overflow="wrap" lineNumbers="true" %}
```java
Method getMeid = getHiddenMethod("getMeid", TelephonyManager.class, new Class[]{int.class});
        meid = (String) getMeid.invoke(mTelephonyManager, 0);

public Method getHiddenMethod(String methodName, Class fromClass, Class[] params) {
        Method method = null;
        try {
            Class clazz = Class.forName(fromClass.getName());
            method = clazz.getMethod(methodName, params);
            method.setAccessible(true);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        }

        return method;
    }
```
{% endcode %}

#### Important Considerations

* CDMA SIM Card Requirement: To successfully retrieve the MEID, ensure that a CDMA SIM card is inserted into the terminal. The MEID can be retrieved regardless of which slot the CDMA SIM card is inserted into.
* MEID Display in Settings: Once the CDMA SIM card is inserted and the terminal recognizes it, the MEID can be viewed in the terminal's settings menu, typically listed under 'MEID (Slot 1)'.
