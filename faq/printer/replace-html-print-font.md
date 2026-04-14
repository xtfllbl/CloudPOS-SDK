# Replace HTML Print Font

### Copying the Font File

* **Font File Selection:** Choose the desired font file (e.g., **'ABC.TTF**').
* **Destination:** Copy this file to the **'assets**' folder of your application project.

### Implementing the Font in HTML Content

{% code overflow="wrap" lineNumbers="true" %}
```html
<!DOCTYPE html>
<html>
<head>
    <style type="text/css">
        @font-face {
            font-family:TestFont;
            src:url('file:///android_asset/ABC.TTF');
        }
        #div1 {
            font-family:TestFont;
            font-size  :30px;
        }
    </style>
</head>
<body>
<!--add picture-->
<!--<img src="file:///android_asset/cloudpos.png">-->
<h2>For example,custom font:</h2>
<div id="div1">
    We use smart solution to
    <br/>
    connect business and
    <br/>
    customers!
    <br/>
    What We Do?
    <br/>
    wizarPOS
    Connect Business
    and Customers
    With Innovations
    <br/>
    WizarPOS is dedicated to developing
    secure, trusted, affordable and intelligent
    product platform to enable innovations
    in the business world.
</div>
It has many functions.Waiting for you to find out!
</body>
</html>
```
{% endcode %}
