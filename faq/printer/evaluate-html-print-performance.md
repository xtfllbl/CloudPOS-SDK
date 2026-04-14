# Evaluate HTML Print Performance

### Initial Bitmap Generation from HTML:

* **First Use:** Approximately 1 second to generate a bitmap from HTML.
* **Subsequent Uses:** Each subsequent generation takes about 0.5 seconds.

### Performance in Different Scenarios:

* **Printing 60-Line Tickets:**
  * Start Time: Printing begins 1 second (or 0.5 second) later than in text mode.
  * Stop Time: Printing ends 0.5 second (or 0.2 second) later than in text mode.
* **Printing 120-Line Tickets:**
  * Start Time: Printing begins 1 second (or 0.5 second) later than in text mode.
  * Stop Time: Printing ends 0.5 second earlier than in text mode.
* **Printing 70cm Tickets:**
  * Preparation: Ready to print the image in approximately 1.5 seconds.
  * Total Printing Time: Around 13 seconds.

### Optimization Strategies:

* **Content Simplification:** Keep HTML content as straightforward as possible.
* **Tag Management:** The number of tags in HTML affects bitmap rendering speed. Use the minimum number of necessary tags.

### Demonstration and Resources:

* **Demo Availability:** For practical demonstration and further understanding, please download the provided [demo](https://ftp.wizarpos.com/advanceSDK/PrinterModelDemo.zip).
