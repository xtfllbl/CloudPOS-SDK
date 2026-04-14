# Set Network Operators API

### Permission

The application declares the following permissions in the manifest：

```java
 android.permission.CLOUDPOS_SET_CELLULAR_NETWORK_OPERATOR
```

### Description

* Bind Service

{% code overflow="wrap" lineNumbers="true" %}
```java
bindService(new Intent().setClassName("com.smartpos.phone.settings", "com.smartpos.phone.settings.RadioQueryService"), mQueryRadioNetworkConnection, Context.BIND_AUTO_CREATE);
```
{% endcode %}

* Use the IBinder returned by the service to construct the communication Messenger

{% code overflow="wrap" lineNumbers="true" %}
```java
private ServiceConnection mQueryRadioNetworkConnection = new ServiceConnection() {
@Override
public void onServiceDisconnected(ComponentName name) {
mService = null;
}
```
{% endcode %}

* Define a Client Messenger associated with the Handler to receive the return from the server:

{% code overflow="wrap" lineNumbers="true" %}
```java
/** Target we publish for clients to send messages to IncomingHandler.
*/
final Messenger mMessenger = new Messenger(new IncomingHandler());

/* * Start cellular network operator querying. * @param event the event you want to start, can be one of following: * 1 - EVENT_NETWORK_SCAN * 2 - EVENT_NETWORK_SELECT * @return mMessenger which associated with Handler.
*/
Message msg = Message.obtain(null, 1 / event /, 0 / slot */, 0);
msg.replyTo = mMessenger;
mService.send(msg);

/** Receive the return of the network operator's search interface:*/
final String[] scanInfo = msg.getData().getStringArray("result");
for (int i = 0; i < scanInfo.length; i++) {
String item[] = scanInfo[i].split(",");
String operatorAlphaLong = scanInfo0; // such as 'CHN-UNICOM'
String operatorAlphaShort = scanInfo1; // such as 'UNICOM'
String operatorNumeric = scanInfo2; // such as '46001'
String stateString = scanInfo3; // such as 'available/forbidden'
}

/** Set cellular network operator. * @param event the event you want to start, can be one of following: * 1 - EVENT_NETWORK_SCAN * 2 - EVENT_NETWORK_SELECT * @return mMessenger which associated with Handler.
*/
Bundle bundle = new Bundle();
bundle.putString("operatorAlphaLong", operatorAlphaLong);
bundle.putString("operatorAlphaShort", operatorAlphaShort);
bundle.putString("operatorNumeric", operatorNumeric);
bundle.putString("stateString", stateString);
Message msg = Message.obtain(null, 2 / event /, 0 / slot */, 0, bundle);
msg.replyTo = mMessenger;
mService.send(msg);

/** Return of the interface set:*/
String responce = "Registration Done";
switch (msg.arg1) {
case -1:
responce = "Not Allowed";
break;
case -2:
responce = "Please connect later";
break;
}
@Override
public void onServiceConnected(ComponentName name, IBinder service) {
// Messenger for communicating with service
Messenger mService = new Messenger(service);
}
};
```
{% endcode %}

### Sample code

{% code overflow="wrap" lineNumbers="true" %}
```java
public class QueryRadioActivity extends Activity {
	private static final String TAG = "QueryRadioActivity";
	// static events
    private static final int EVENT_NETWORK_SCAN = 1;
    private static final int EVENT_NETWORK_SELECT = 2;
    private static final int EVENT_NETWORK_SCAN_COMPLETED = 3;
    private static final int EVENT_NETWORK_SELECTION_DONE = 4;
    private static final int QUERY_OK = 0;
    private static final int QUERY_PARTIAL = 1;
    private static final int QUERY_IS_RUNNING = -2;
    private static final int SELECT_OK = 0;
    private static final int SELECT_DENIED = -1;
    private static final int SELECT_BUSY = -2;
	private ProgressDialog mProgressDialog;
	//map of RAT type values to user understandable strings
    private HashMap<String, String> mRatMap = new HashMap<String, String>();
	
	private ServiceConnection mQueryRadioNetworkConnection = new ServiceConnection() {
		
		@Override
		public void onServiceDisconnected(ComponentName name) {
			mService = null;
		}
		
		@Override
		public void onServiceConnected(ComponentName name, IBinder service) {
			mService = new Messenger(service);
		}
	};
	
	/**
     * Handler of incoming messages from service.
     */
    class IncomingHandler extends Handler {
		@Override
		public void handleMessage(Message msg) {
			mProgressDialog.dismiss();
			String responce = "Unknown response";
			switch (msg.what) {
			case EVENT_NETWORK_SCAN_COMPLETED: // Querying done.
				switch (msg.arg1) {
                case QUERY_OK:
                case QUERY_PARTIAL:
                	responce = "Query response is OK!";
                	final String[] scanInfo = msg.getData().getStringArray("result");
                    AlertDialog.Builder builder = new AlertDialog.Builder(QueryRadioActivity.this);
                    // emmmmmmmmmmmmm
                    String[] items = new String[scanInfo.length];
                    String operatorNumeric;
                    int operatorNumericIndexOf;
                    String item[];
                    for (int i = 0; i < scanInfo.length; i++) {
                    	item = scanInfo[i].split(",");
                    	operatorNumeric = item[2];
                    	operatorNumericIndexOf = operatorNumeric.indexOf("+") + 1;
                    	operatorNumeric = operatorNumeric.substring(0, operatorNumericIndexOf) + " " + mRatMap.get(operatorNumeric.substring(operatorNumericIndexOf, operatorNumeric.length()));
                    	items[i] = item[0] + " " + operatorNumeric + " " + item[3];
                    }
                    
                    builder.setItems(items, new OnClickListener() {

                        @Override
                        public void onClick(DialogInterface dialog, int which) {
                        	try {
                        		Bundle bundle = new Bundle();
                        		String item[] = scanInfo[which].split(",");
                        	    bundle.putString("operatorAlphaLong", item[0]); // such as 'CHN-UNICOM'
                        	    bundle.putString("operatorAlphaShort", item[1]); // such as 'UNICOM'
                        	    bundle.putString("operatorNumeric", item[2]); // such as '46001'+14(RIL_RADIO_TECHNOLOGY_LTE)
                        	    bundle.putString("stateString", item[3]); // such as 'available/forbidden'
                        		Message msg = Message.obtain(null, EVENT_NETWORK_SELECT, 0 /* slot */, 0, bundle);
                				msg.replyTo = mMessenger;
                				mService.send(msg);
                				mProgressDialog = ProgressDialog.show(QueryRadioActivity.this, "", "Selecting, please wait..", true, true);
    						} catch (RemoteException e) {
    							e.printStackTrace();
    						}
                        }
                    });
                    builder.show();
                	break;
                case QUERY_IS_RUNNING:
                	responce = "Query is running, please retry later!";
                	break;
            	default:
            		/* In case of one of following:
					 *        int QUERY_EXCEPTION = -1;
					 *        int QUERY_ABORT = 2;
					 *        int QUERY_REJ_IN_RLF = 3;
            	     */
            		responce = "Busy, please query later!";
            		break;
				}
				break;

			case EVENT_NETWORK_SELECTION_DONE: // Select done.
				switch (msg.arg1) {
				case SELECT_OK:
					responce = "Registration Done";
					break;
				case SELECT_DENIED:
					responce = "Not Allowed";
					break;
				case SELECT_BUSY:
					responce = "Please connect later!";
					break;
				}
				break;
			}
			Toast.makeText(QueryRadioActivity.this, responce, Toast.LENGTH_LONG).show();
		}
	};
	
	/** Messenger for communicating with service. */
    Messenger mService = null;
	
	/**
     * Target we publish for clients to send messages to IncomingHandler.
     */
    final Messenger mMessenger = new Messenger(new IncomingHandler());
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.query_radio);
		mRatMap.put("0" /* RIL_RADIO_TECHNOLOGY_UNKNOWN */, "Unknown");
	    mRatMap.put("1" /* RIL_RADIO_TECHNOLOGY_GPRS */, "2G");
	    mRatMap.put("2" /* RIL_RADIO_TECHNOLOGY_EDGE */, "2G");
	    mRatMap.put("3" /* RIL_RADIO_TECHNOLOGY_UMTS */, "3G");
	    mRatMap.put("4" /* RIL_RADIO_TECHNOLOGY_IS95A */, "2G");
	    mRatMap.put("5" /* RIL_RADIO_TECHNOLOGY_IS95B */, "2G");
	    mRatMap.put("6" /* RIL_RADIO_TECHNOLOGY_1xRTT */, "2G");
	    mRatMap.put("7" /* RIL_RADIO_TECHNOLOGY_EVDO_0 */, "3G");
	    mRatMap.put("8" /* RIL_RADIO_TECHNOLOGY_EVDO_A */, "3G");
	    mRatMap.put("9" /* RIL_RADIO_TECHNOLOGY_HSDPA */, "3G");
	    mRatMap.put("10" /* RIL_RADIO_TECHNOLOGY_HSUPA */, "3G");
	    mRatMap.put("11" /* RIL_RADIO_TECHNOLOGY_HSPA */, "3G");
	    mRatMap.put("12" /* RIL_RADIO_TECHNOLOGY_EVDO_B */, "3G");
	    mRatMap.put("13" /* RIL_RADIO_TECHNOLOGY_EHRPD */, "3G");
	    mRatMap.put("14" /* RIL_RADIO_TECHNOLOGY_LTE */, "4G");
	    mRatMap.put("19" /* RIL_RADIO_TECHNOLOGY_LTE_CA */, "4G");
	    mRatMap.put("15" /* RIL_RADIO_TECHNOLOGY_HSPAP */, "3G");
	    mRatMap.put("16" /* RIL_RADIO_TECHNOLOGY_GSM */, "2G");
	    mRatMap.put("17" /* RIL_RADIO_TECHNOLOGY_TD_SCDMA */, "3G");
		findViewById(R.id.query_radio_network).setOnClickListener(new View.OnClickListener() {
			
			@Override
			public void onClick(View v) {
				if (mService == null) {
					Log.w(TAG, "Query failed, could't bind service.");
					Toast.makeText(QueryRadioActivity.this, "Query failed, could't bind service.", Toast.LENGTH_LONG).show();
					return;
				}
				try {
					Message msg = Message.obtain(null, EVENT_NETWORK_SCAN /* event */, 0 /* slot */, 0);
					msg.replyTo = mMessenger;
					mService.send(msg);
					mProgressDialog = ProgressDialog.show(QueryRadioActivity.this, "", "Querying, please wait..", true, true);
				} catch (RemoteException e) {
					e.printStackTrace();
				}
			}
		});
		bindService(new Intent().setClassName("com.smartpos.phone.settings", "com.smartpos.phone.settings.RadioQueryService"), mQueryRadioNetworkConnection, Context.BIND_AUTO_CREATE);
	}
	
	@Override
    protected void onDestroy() {
        super.onDestroy();
        unbindService(mQueryRadioNetworkConnection);
    }
}
```
{% endcode %}
