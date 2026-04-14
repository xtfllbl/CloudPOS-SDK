# Accessory Agent Service D22/Q3

### Introduction

The D22 device can establish a USB connection with the Q3, where D22 operates in master mode and Q3 in slave mode. The AccessoryConnectionAgent APK facilitates communication between applications across these two devices using Intents sent through the USB connection.

### User Manual

* For detailed instructions on how to use the Accessory Connection Agent service, refer to the [Accessory Connection Agent service user manual](https://ftp.wizarpos.com/advanceSDK/AccessoryConnectAgentusermanual.pdf).

### Demonstration and Development:

1. **Demo for APK Development:**
   * Explore the demo for insights into developing APKs for this setup, [Access AccessoryAgentDemo](https://github.com/SmartPOSSamples/AccessoryAgentDemo).
2. **Testing APK:**
   * After installation and running this APK, it will send an intent via the USB connection to initiate the merchant self-test application on the other device, [Download AccessoryConnectionAgentDemo APK](https://ftp.wizarpos.com/advanceSDK/AccessoryConnectionAgentDemo.apk).

**Sender snippet code:**

{% code overflow="wrap" lineNumbers="true" %}
```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initView();
        bindServer();
    }

    private void initView() {
        bindServerStatus = findViewById(R.id.bindServerStatus);
        startActivity = findViewById(R.id.startActivity);
        String json ="{\n" +
                "    \"action\": \"android.intent.action.MAIN\",\n" +
                "    \"className\": \"com.wizarpos.accessoryreceiveintentdemo.MainActivity\",\n" +
                "    \"flags\": 268435456,\n" +
                "    \"packageName\": \"com.wizarpos.accessoryreceiveintentdemo\",\n" +
                "    \"putExtra\": {\n" +
                "        \"extraData\": \"10\"\n" +
                "    }\n" +
                "}";
        startActivity.setOnClickListener(v -> {
            if(remoteServe != null){
                try {
                    remoteServe.remoteIntent(json);
                } catch (RemoteException e) {
                    throw new RuntimeException(e);
                }
            }else {
                Toast.makeText(this, "The AIDL service is disconnected", Toast.LENGTH_SHORT).show();
            }

        });
    }

    private void bindServer() {
        Intent intent = new Intent();
        ComponentName componentName =new ComponentName(INTENT_PACKAGE, INTENT_ACTION);
        intent.setComponent(componentName);
        bindService(intent, mServiceConnection, BIND_AUTO_CREATE);
    }
    ServiceConnection mServiceConnection = new ServiceConnection() {

        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            remoteServe = IRemoteAccessoryApi.Stub.asInterface(service);
            bindServerStatus.setText("The AIDL service is Connected");
        }

        @Override
        public void onServiceDisconnected(ComponentName name) {
            remoteServe = null;
            bindServerStatus.setText("The AIDL service is disconnected");
        }
    };

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unbindService(mServiceConnection);
    }
```
{% endcode %}

**Receiver(com.wizarpos.accessoryreceiveintentdemo) snippet code:**

{% code overflow="wrap" lineNumbers="true" %}
```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //Receive intent data
        String extraData = getIntent().getStringExtra("extraData");
    }

    @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        //Receive intent data
        String extraData = intent.getStringExtra("extraData");
    }
```
{% endcode %}

### AccessoryConnectionAgent Service APK

**Installation Requirements:**

* The AccessoryConnectAgent is typically included in the firmware (FW) of D22 and Q3. For older firmware versions, developers may need to install the agent manually. [Download Connection Agent service APK](https://ftp.wizarpos.com/advanceSDK/AccessoryAgentHostService-master-release-v1.0.26-r20240606172311-q1_platform.apk).

### Initiating USB Connection Mode in Development:

*   **Enabling AccessoryConnectionAgent:**

    * By default, the AccessoryConnectionAgent is disabled. Developers can use the provided APK to enable it.
    * For production firmware, the agent is initialized before factory release.
    * [Download Initialize APK](https://ftp.wizarpos.com/advanceSDK/InitConnectionMode.apk) for D22 and Q3.


* **Mode Selection:**
  * In Q3, the default mode is set to slave, while other devices default to master mode.
* **Usbchannel Switch:**
  * Enable or disable the Accessory Connection Agent service as needed for your development and testing purposes.

### Test APKs between D3 and Q3

* [Download Initialize APK ](https://ftp.wizarpos.com/advanceSDK/InitConnectionMode_d3.apk)for D3. Set mode and enable USB connectiong in D3. Initialize APK for Q3, please use the [APK describe in Initating USB Connection Mode in Development](accessory-agent-service-d22-q3.md#initiating-usb-connection-mode-in-development).
* [Testing APK](https://ftp.wizarpos.com/advanceSDK/AccessoryConnectionAgentTestdemo-q1_platform.apk). Another testing APK, after installation and running this APK, it will send an intent via the USB connection to initiate the initialize application on the other device. This APK can also test between D22 and Q3 too.&#x20;

### [Payment Demo between D22 and Q3](https://ftp.wizarpos.com/advanceSDK/D22_Q3_PaymentDemo_20241231.zip)

Includes two demos, one running in D22, one running in Q3.



This guide provides essential information for developers and users to set up and use the Accessory Agent Service between D22 and Q3 devices, ensuring efficient and effective communication and testing.

If you are looking for more solutions, please refer to:

{% content-ref url="https://app.gitbook.com/s/Y7FuzH91SaNfvhwFA9Ic/choose-your-best-practice" %}
[Choose Your Best Practice](https://app.gitbook.com/s/Y7FuzH91SaNfvhwFA9Ic/choose-your-best-practice)
{% endcontent-ref %}
