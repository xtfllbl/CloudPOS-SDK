# Use Terminal Camera

### Introduction:

This guide explains how to enable your application to access and use the camera functionality of a terminal device using the Android SDK. Please refer to [the document](https://developer.android.com/media/camera/camera2)

### Understanding Camera IDs:

* When you use the command 'camera.open(ID)', it's important to note that the ID values vary across different terminal models.
* Refer to the provided table for the specific ID definitions corresponding to each product model.

| Product Model | Camera ID                                   |
| ------------- | ------------------------------------------- |
| W1            | 0                                           |
| W1V2          | 0                                           |
| Q1            | 0: zoom camera, 1: fixed focus camera       |
| Q1V2          | 0: zoom/zebra camera, 1: fixed focus camera |
| Q2            | 0: back camera, 1: front camera             |
| K2            | 0                                           |
| PAD1          | 0                                           |
| Q3            | 0: back camera, 1: front camera             |

### Demo Application for Reference:

* We have developed a demo application that illustrates how to implement the photographing function.
* Please [download the demo](https://github.com/SmartPOSSamples/PhotographDemo) for a practical example and better understanding.
