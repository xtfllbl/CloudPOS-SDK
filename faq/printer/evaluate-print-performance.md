# Evaluate Print Performance

### Objective:

This document provides a detailed analysis of the terminal's printing performance, focusing on the time efficiency of the print process.

### Performance Metrics:

1. **Initiation Time (Column 3):**
   * **Description:** This metric indicates the duration from the moment the print method is called to when the paper starts moving.
   * **Purpose:** It helps in assessing the response time of the printer after receiving a print command.
2. **Completion Time (Column 4):**
   * **Description:** This metric shows the time taken from the initiation of the print method until the completion of the printing process.
   * **Purpose:** It evaluates the overall efficiency of the printing process, from start to finish.

### Further Queries:

* **Q2:**

<table data-full-width="false"><thead><tr><th width="146">print method</th><th>receipt length</th><th>start feeding paper (s)</th><th>print finish/method return (s)</th><th>feeding speed (mm/s)</th></tr></thead><tbody><tr><td>printText</td><td>60 lines/~30 cm</td><td>0.1</td><td>5.5</td><td>~54</td></tr><tr><td>printText</td><td>120 lines/~60 cm</td><td>0.2</td><td>11.3</td><td>~53</td></tr><tr><td>printBitmap</td><td>25 cm</td><td>0.3</td><td>3.6</td><td>~69</td></tr><tr><td>printBitmap</td><td>50 cm</td><td>0.4</td><td>7.6</td><td>~66</td></tr><tr><td>printBitmap</td><td>75 cm</td><td>0.6</td><td>11.6</td><td>~65</td></tr><tr><td>printHTML</td><td>25 cm</td><td>1.3</td><td>4.7</td><td>~53</td></tr><tr><td>printHTML</td><td>50 cm</td><td>1.5</td><td>8.8</td><td>~57</td></tr><tr><td>printHTML</td><td>75 cm</td><td>1.6</td><td>12.7</td><td>~59</td></tr></tbody></table>

* **Q1v2:**

| print method | receipt length    | start feeding paper(s) | print finish/method return (s) | feeding speed (mm/s) |
| ------------ | ----------------- | ---------------------- | ------------------------------ | -------------------- |
| printText    | 60 lines/\~30 cm  | 0.1                    | 6.3                            | \~47                 |
| printText    | 120 lines/\~60 cm | 0.2                    | 12.6                           | \~47                 |
| printBitmap  | 25 cm             | 0.3                    | 4.5                            | \~55                 |
| printBitmap  | 50 cm             | 0.4                    | 8.9                            | \~56                 |
| printBitmap  | 75 cm             | 0.5                    | 13.6                           | \~55                 |
| printHTML    | 25 cm             | 1.2                    | 5.7                            | \~44                 |
| printHTML    | 50 cm             | 1.3                    | 10                             | \~50                 |
| printHTML    | 75 cm             | 1.4                    | 14                             | \~54                 |
