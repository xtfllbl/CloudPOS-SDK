# Obtain Signal Strength

### Overview

This guide demonstrates how to use the 'PhoneStateListener' class in Android to monitor and retrieve the signal strength of a mobile device. This is particularly useful for applications that need to track network quality or adjust functionalities based on signal strength.

### Code Snippet

{% code overflow="wrap" lineNumbers="true" %}
```java
   
    public TelephonyManager telephoneManager;
    public PhoneStateListener phoneStateListener;

    public void listenerSignal(Context context) {
        telephoneManager = (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE);
				telephoneManager.listen(phoneStateListener,
       
        phoneStateListener = new PhoneStateListener() {
            @Override
            public void onServiceStateChanged(ServiceState serviceState) {
                Logger.debug("onServiceStateChanged++++");
                super.onServiceStateChanged(serviceState);
                int voiceRegState = serviceState.getVoiceRegState();
                int dataRegState = serviceState.getDataRegState();
            }


            @Override
            public void onSignalStrengthsChanged(SignalStrength signalStrength) {
                Logger.debug("onSignalStrengthsChanged++++");
                super.onSignalStrengthsChanged(signalStrength);

                int level = signalStrength.getLevel();//Call requires API level 23
                int asu = getMethod(signalStrength, "getAsuLevel");//Hide
                int dbm = getMethod(signalStrength, "getDbm");//Hide
            }


        };

        telephoneManager.listen(phoneStateListener,
        PhoneStateListener.LISTEN_SERVICE_STATE
                | PhoneStateListener.LISTEN_SIGNAL_STRENGTHS
                | PhoneStateListener.LISTEN_CALL_STATE
                | PhoneStateListener.LISTEN_DATA_CONNECTION_STATE
                | PhoneStateListener.LISTEN_DATA_ACTIVITY);

    }


    int getMethod(SignalStrength signalStrength, String name) {
        Class<?> clazz = signalStrength.getClass();
        Method method = null;
        int i = 0;
        try {
            method = clazz.getMethod(name);//getDbm
            Object result = method.invoke(signalStrength);
            i = Integer.parseInt(String.valueOf(result));
        } catch (Exception e) {
            e.printStackTrace();
        }
        return i;
    }
```
{% endcode %}
