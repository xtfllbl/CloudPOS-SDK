# Connect wirelessly

1. Find the IP address of the terminal at **Settings** > **About POS** > **Status** > **IP address**.
2.  Connect to the terminal by its IP address:

    ```
    $ adb connect device_ip_address

    ```


3. Confirm that your host computer is connected to the target terminal:

```sh
// after run adb connect, result is:
connected to device_ip_address:55555
```

<pre class="language-sh"><code class="lang-sh"><strong>// or use the follow command to confirm again:
</strong><strong>$ adb devices
</strong>List of devices attached
device_ip_address:5555 device
</code></pre>

Your device is now connected to `adb`.
