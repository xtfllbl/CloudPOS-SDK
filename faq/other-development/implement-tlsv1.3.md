# Implement TLSv1.3

### Overview

This guide provides resources and instructions on how to implement TLSv1.3, the latest version of the Transport Layer Security protocol, in your applications for enhanced security.

### Resources and References

* GitHub Project:
  * Access a relevant [GitHub project](https://github.com/google/conscrypt) that provides detailed examples or libraries for implementing TLSv1.3.
* Additional Resources:
  * List any other [Resouces](https://source.android.google.cn/devices/architecture/modular-system/conscrypt#conscrypt-format) that might be helpful for understanding and implementing TLSv1.3.

### Sample Code Snippet

* Include a brief description or title of the sample snippet.

{% code overflow="wrap" lineNumbers="true" %}
```java
    /**
     * dependencies implementation 'org.conscrypt:conscrypt-android:2.5.2'
     * @param url
     */
    private void tlsv13(String url) {
        Provider conscrypt = Conscrypt.newProvider();
        try {
            SSLContext context = SSLContext.getInstance("TLSv1.3",conscrypt);
            context.init(null/*keyManagers*/, null /*new CtsTrustManager[] {trustManager}*/, null);
            SSLSocketFactory factory = context.getSocketFactory();
            URL sslURL = new URL(url);
            HttpsURLConnection con = (HttpsURLConnection) sslURL.openConnection();
            con.setSSLSocketFactory(factory);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
{% endcode %}

### Demo Application

* For a practical demonstration of TLSv1.3 in action, download the provided [demo](https://github.com/SmartPOSSamples/Tlsv1.3demo.git).
