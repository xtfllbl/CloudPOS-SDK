# Best Practices for Printer

## Brief explanation

When programming for the printer in a multi-threaded environment on WizarPOS terminals, the most critical factor is the **exclusive access** nature of the hardware. The system does not allow multiple threads or applications to open and operate the printer device simultaneously.

Below are the specific programming recommendations based on the provided technical documentation:

#### 1. Serialize Printing Tasks

Because the printer device is exclusive, attempting to call `open()` while it is already in use by another thread or application will result in error code `0x57` ("Too many users"), indicating the device is occupied. You should implement a **single-thread task queue** (e.g., using `SingleThreadExecutor` or `HandlerThread`) to handle all print requests sequentially.

#### 2. Unified Open-Print-Close Sequence

For a consistent output, it is a best practice to call `open()` once at the start of a transaction, send all relevant print commands (text, images, and QR codes) in a continuous stream, and call `close()` only when the job is complete. This prevents other threads or processes from "inserting" unwanted content in the middle of a receipt.

#### 3. Precise Completion Detection

Avoid calling `close()` immediately after the last print command, as the physical hardware may still be feeding paper.

* **On newer models (like Q2 Premium):** Use the `isPrintingDone(int timeoutMS)` API to accurately determine when physical printing has finished.
* **On older models:** Call `queryStatus()` after your print commands; since commands are executed sequentially, the return of this method serves as a proxy for the completion of previous tasks.

#### 4. Lifecycle and Resource Management

Strictly manage the device lifecycle by placing the `close()` call within a `finally` block to ensure the resource is released even if an exception occurs. Furthermore, ensure that the printer is explicitly closed during the `onPause()` or `onDestroy()` lifecycle methods of your Android components to prevent resource leaks that block other applications.

#### 5. Performance and Buffer Optimization

For large receipts or high-resolution bitmaps, consider "segmented printing" to avoid lag and potential buffer issues. In cases where status feedback is limited, adding a small delay (e.g., 2 seconds) between large bitmap blocks can help the printer catch up and prevent garbled output.

#### 6. Inter-App Coordination

If your solution involves multiple independent apps, you should design a centralized **printer management service** using the Android Binder mechanism or a `ContentProvider` to coordinate access and queue tasks across different processes.

## Multi-threaded Printer Programming Best Practices

When calling a printer (`PrinterDevice`) in a multi-threaded environment, directly calling `open()` in each thread will cause the following problems:

1. **Underlying state conflicts**: The SDK's `open()` method will throw a `DeviceException` when the device is already open (such as `BAD_CONTROL_MODE` / device already opened).
2. **Scrambled print content**: The printer is a physical serial device. Multiple threads printing at the same time will cause data from different threads to interleave and become scrambled.

The following are 3 common solutions to avoid repeated `open()` and ensure multi-thread safety.

{% hint style="success" %}
**Recommendation**: Solution 1 (single-threaded task queue) is the best practice for POS printer development.
{% endhint %}

***

### Solution 1: Single-threaded Task Queue (Recommended, Best Practice)

Submit all print tasks to a single-threaded thread pool for serial execution, and let the queue uniformly manage `open`, printing, and `close`.

```java
import com.cloudpos.DeviceException;
import com.cloudpos.POSTerminal;
import com.cloudpos.printer.PrinterDevice;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class PrinterManager {
    private static PrinterManager instance;
    private PrinterDevice printerDevice;
    // Single-thread pool to ensure all print tasks are executed serially in order
    private final ExecutorService printExecutor = Executors.newSingleThreadExecutor();

    private PrinterManager() {
    }

    public static synchronized PrinterManager getInstance() {
        if (instance == null) {
            instance = new PrinterManager();
        }
        return instance;
    }

    private PrinterDevice getDevice() {
        if (printerDevice == null) {
            printerDevice = (PrinterDevice) POSTerminal.getInstance()
                    .getDevice("com.cloudpos.device.printer");
        }
        return printerDevice;
    }

    /**
     * Asynchronously submit a print task (can be called concurrently by multiple threads)
     */
    public void executePrintTask(PrintTask task) {
        printExecutor.submit(() -> {
            PrinterDevice device = getDevice();
            try {
                // Open is performed uniformly within the single-threaded queue
                device.open();

                // Execute the specific print logic
                task.onPrint(device);

            } catch (DeviceException e) {
                e.printStackTrace();
            } finally {
                try {
                    device.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public interface PrintTask {
        void onPrint(PrinterDevice device) throws DeviceException;
    }
}
```

**Usage example:**

```java
// Thread A
PrinterManager.getInstance().executePrintTask(device -> {
    device.printText("======== Bill A ========\n");
});

// Thread B (concurrent call)
PrinterManager.getInstance().executePrintTask(device -> {
    device.printText("======== Bill B ========\n");
});
```

***

### Solution 2: Reference Counting

Suitable for scenarios where the device needs to be opened and closed dynamically. If multiple business modules have inconsistent lifecycles and `open`/`close` need to be managed manually, reference counting + locking can be used.

```java
import com.cloudpos.DeviceException;
import com.cloudpos.POSTerminal;
import com.cloudpos.printer.PrinterDevice;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.locks.ReentrantLock;

public class PrinterReferenceManager {
    private static PrinterReferenceManager instance;
    private PrinterDevice printerDevice;
    private final AtomicInteger refCount = new AtomicInteger(0);
    private final ReentrantLock lock = new ReentrantLock();

    public static synchronized PrinterReferenceManager getInstance() {
        if (instance == null) {
            instance = new PrinterReferenceManager();
        }
        return instance;
    }

    public PrinterDevice openPrinter() throws DeviceException {
        lock.lock();
        try {
            if (printerDevice == null) {
                printerDevice = (PrinterDevice) POSTerminal.getInstance()
                        .getDevice("com.cloudpos.device.printer");
            }
            // Only trigger the actual open when the first thread/module calls it
            if (refCount.getAndIncrement() == 0) {
                printerDevice.open();
            }
            return printerDevice;
        } finally {
            lock.unlock();
        }
    }

    public void closePrinter() {
        lock.lock();
        try {
            // Only trigger the actual close when all references are released
            if (refCount.decrementAndGet() == 0 && printerDevice != null) {
                try {
                    printerDevice.close();
                } catch (DeviceException e) {
                    e.printStackTrace();
                }
            }
            if (refCount.get() < 0) {
                refCount.set(0); // Prevent excessive close calls from causing a negative count
            }
        } finally {
            lock.unlock();
        }
    }
}
```

***

### Solution 3: Catch and Ignore the Already-open Exception

Simple protection. If `open()` must be called in multiple places in the business code, you can avoid crashes by checking or catching exceptions, but you still need to use a lock (`Synchronized`/`Lock`) to prevent concurrent races.

```java
public synchronized void safeOpen(PrinterDevice device) {
    try {
        device.open();
    } catch (DeviceException e) {
        // -254 or BAD_CONTROL_MODE means the device is already open and can be safely ignored
        if (e.getCode() == DeviceException.BAD_CONTROL_MODE) {
            // Already open, ignore
        } else {
            e.printStackTrace();
        }
    }
}
```

***

### Comparison of Solutions

| Solution                 | Repeated `open()` Prevention | Print Order Guarantee | Complexity | Recommended Scenario              |
| ------------------------ | ---------------------------- | --------------------- | ---------- | --------------------------------- |
| 1. Single-threaded queue | ✅                            | ✅                     | Low        | Most POS printing scenarios       |
| 2. Reference counting    | ✅                            | ⚠️ (needs extra sync) | Medium     | Dynamic open/close across modules |
| 3. Catch and ignore      | ⚠️ (partial)                 | ❌                     | Low        | Simple protection only            |

***

### Summary and Recommendation

{% hint style="success" %}
**Solution 1 (single-threaded task queue) is strongly recommended.**

It not only solves the problem of repeated `open()`, but also ensures that receipt print content is not scrambled, and is the standard practice for POS printer development.
{% endhint %}
