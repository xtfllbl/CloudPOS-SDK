# Understanding Image Print Gaps

### Issue Description:

When printing images continuously on a receipt, a small blank line may appear between the first and second image.

### Cause:

* **Default Driver Configuration:** The printer driver is configured to process images in segments of 24-dot lines.
* **Image Height Alignment:** If the height of the first image is not an exact multiple of 24 dots, the driver will align the image to the nearest 24-dot line. This alignment results in a blank line, the width of which is determined by the remainder of the height divided by 24.
