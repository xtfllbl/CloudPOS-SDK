# Use Terminal Bluetooth Printer

### Initial Setup:

Not all terminals come with the Bluetooth printer service pre-installed. Before proceeding, ensure you download and install the bluetooth printer service APK.

* [Bluetooth printer service APK for Q1, Q2 Android 6/7, Q3](https://ftp.wizarpos.com/advanceSDK/VirtualPrintService-release-v1.0.1-r20240927174600-VirtualPrintServiceOnlyAndroid6_7-q1_releasekey.apk).
* [Bluetooth printer service APK for Q2 Android 12](https://ftp.wizarpos.com/advanceSDK/VirtualPrintService-release-v1.1.11-r20240927171753-master-q1_platform.apk).

### Settings configuration:

1. Navigate to **Settings** > **Connected devices or drop down in the screen, click Bluetooth icon button** to access the _Connected devices_ page.
2. Select **Connection preferences** > **Printing**, then disable **Default Print Service** and ensure **CloudPOSPrinterService** is enabled.
3. Tap **Pair new device**.
4. From the _Available devices_ list, choose **CloudPOS\_Printer**.
5. Verify that **CloudPOS\_Printer** appears under _Saved devices_.

### Service Overview:

The Bluetooth printer service facilitates printing images and text using Bluetooth APIs. This service operates by connecting with Bluetooth printers and sending data for printing. Data is typically formatted as image and text documents.

### Service Startup Process:

1. **Turning on Bluetooth:** Automatically activates Bluetooth if it's not already on.
2. **Scanning for Devices:** Discovers nearby Bluetooth devices.
3. **Pairing:** Selects and pairs with a Bluetooth printer.
4. **Connecting:** Establishes a connection using the Serial Port Profile (SPP).
5. **Data Transmission:** Sends data in the form of ESC commands.
6. **Printing:** Executes the print command for the transmitted data.

### Prerequisites for Use:

* Android SDK 24
* Android Build Tools v27.0.0
* Android Support Repository
* &#x20;ZXing (for barcode processing)

### Getting Started with Development:

To build the Bluetooth printer service, you can use Gradle. Execute the gradle build command or use the "Import Project" option in Android Studio to get started.

### Code snippet

* **Basic API of Bluetooth**

{% code overflow="wrap" lineNumbers="true" %}
```java
    public void openBluetooth(Activity activity) {
        Intent enableBtIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
        activity.startActivityForResult(enableBtIntent, 1);
    }
    public void closeBluetooth() {
        this.bluetoothAdapter.disable();
    }
    public void searchDevices() {
        this.bluetoothAdapter.startDiscovery();
    }
    private BroadcastReceiver receiver = new BroadcastReceiver() {
        ProgressDialog progressDialog = null;
        @Override
        public void onReceive(Context context, Intent intent) {
            String action = intent.getAction();
            if (BluetoothDevice.ACTION_FOUND.equals(action)) {
                BluetoothDevice device = intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);
                if (device.getBondState() == BluetoothDevice.BOND_BONDED) {
                    addBondDevice(device);
                } else {
                    addUnbondDevice(device);
                }
            } else if (BluetoothDevice.ACTION_ACL_CONNECTED.equals(action)) {
                BluetoothDevice device = intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);
                String msg = "ACTION_ACL_CONNECTED: " + device.getAddress() + "=" + device.getBondState();
                Toast.makeText(context, msg, Toast.LENGTH_LONG).show();
                System.out.println(msg);
            } else if (BluetoothAdapter.ACTION_DISCOVERY_STARTED.equals(action)) {
                progressDialog = ProgressDialog.show(context, "pair...","...", true);
            } else if (BluetoothAdapter.ACTION_DISCOVERY_FINISHED .equals(action)) {
                bluetoothAdapter.cancelDiscovery();
                if (progressDialog != null)
                    progressDialog.dismiss();
                addUnbondDevicesToListView();
                addBondDevicesToListView();
            } else if (BluetoothAdapter.ACTION_STATE_CHANGED.equals(action)) {
                int state = bluetoothAdapter.getState();
                if (state == BluetoothAdapter.STATE_ON) {
                    searchDevices.setEnabled(true);
                    bondDevicesListView.setEnabled(true);
                    unbondDevicesListView.setEnabled(true);
                } else if (state == BluetoothAdapter.STATE_OFF) {
                    searchDevices.setEnabled(false);
                    bondDevicesListView.setEnabled(false);
                    unbondDevicesListView.setEnabled(false);
                } else {
                    System.out.println("Bluetooth.STATE: " + state);
                }
            } else {
                System.out.println("Bluetooth.ACTION: " + action);
            }
        }
    };
```
{% endcode %}

* **Connection with SPP**

{% code overflow="wrap" lineNumbers="true" %}
```java
public boolean connect() {
    if (!isConnected) {
        try {
            bluetoothSocket = createBluetoothSocket();
            bluetoothSocket.connect();
            outputStream = bluetoothSocket.getOutputStream();
            isConnected = bluetoothSocket.isConnected();
            if (this.bluetoothAdapter.isDiscovering()) {
                Toast.makeText(this.context, "success to connect",1).show();
                this.bluetoothAdapter.isDiscovering();
            }
        } catch (Exception e) {
            e.printStackTrace();
            Toast.makeText(this.context, "fail to  connect", 1).show();

            return false;
        }
    }
    Toast.makeText(this.context, this.device.getName() + "connected",Toast.LENGTH_SHORT).show();
    return true;
}

private BluetoothSocket createBluetoothSocket()
        throws IOException, NoSuchMethodException, IllegalAccessException, InvocationTargetException {
    switch (TYPE_OF_CREATING_SOCKET) {
    case 0: return device.createRfcommSocketToServiceRecord(uuid);
    case 1: return device.createInsecureRfcommSocketToServiceRecord(uuid);
    default:
        Method m = device.getClass().getMethod("createRfcommSocket", new Class[] {int.class});
        return (BluetoothSocket) m.invoke(device, 1);
    }
}
```
{% endcode %}

* **Send and Print**

{% code overflow="wrap" lineNumbers="true" %}
```java
final byte[][] byteCommands = { { 0x1b, 0x40 }, //printer commands(ESC commands)
        { 0x1b, 0x4d, 0x00 },
        { 0x1b, 0x4d, 0x01 },
        { 0x1d, 0x21, 0x00 },
        { 0x1d, 0x21, 0x11 },
        { 0x1b, 0x45, 0x00 },
        { 0x1b, 0x45, 0x01 },
        { 0x1b, 0x7b, 0x00 },
        { 0x1b, 0x7b, 0x01 },
        { 0x1d, 0x42, 0x00 },
        { 0x1d, 0x42, 0x01 },
        { 0x1b, 0x56, 0x00 },
        { 0x1b, 0x56, 0x01 },
public void selectCommand() {
    new AlertDialog.Builder(context).setTitle("Commands").setItems(items, new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialog, int which) {
                    if (isConnected) {
                        try {
                            outputStream.write(byteCommands[which]);
                        } catch (IOException e) {
                            Toast.makeText(context, "write exception",Toast.LENGTH_SHORT).show();
                        }
                    } else {
                        Toast.makeText(context, "connection is lost",Toast.LENGTH_SHORT).show();
                    }
                }
            }).create().show();
}
public void write(byte[] buff){
    try {
        outputStream.write(buff);
    } catch (IOException e) {
    }
}
```
{% endcode %}

### Download Bluetooth demo

[Bluetooth Printer APK](https://ftp.wizarpos.com/advanceSDK/bluetoothprintdemo.apk)

[Bluetooth Printer Demo](https://github.com/SmartPOSSamples/BluetoothPrinterDemo)
