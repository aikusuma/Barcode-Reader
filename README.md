Barcode Reader - Google Mobile Vision
===================
Android Barcode Reader library using **Google Mobile Vision.** This library is built on top of google mobile vision sample adding improvements and fixing few bugs.

[ ![Download](https://api.bintray.com/packages/androidhive-info/maven/barcode-reader/images/download.svg) ](https://bintray.com/androidhive-info/maven/barcode-reader/_latestVersion)
[![Example](https://img.shields.io/badge/Example-Movie%20Tickets-green.svg)](https://www.androidhive.info/2017/07/android-implementing-preferences-settings-screen/)

----------

Sample App - Movie Tickets Barcode Scanner
-------------
Below app is built using this library adding few UI improvements to showcase the usefulness of the library. Complete guide to build the app can be read ![here](https://www.androidhive.info/2017/07/android-implementing-preferences-settings-screen/)

Date Picker | Time Picker
--- | ---
![Date Picker](https://user-images.githubusercontent.com/497670/29020592-3a3517bc-7b80-11e7-9803-1395a881a1e7.jpg) | ![Time Picker](https://user-images.githubusercontent.com/497670/29020591-39f0e9b6-7b80-11e7-9251-ea267c53880a.png)


How to Use
-------------
1. Include the barcode reader dependency in app's **build.gradle**
```gradle
dependencies {
    // google mobile vision
    implementation 'com.google.android.gms:play-services-vision:11.0.2'

    // barcode reader
    implementation 'info.androidhive:barcode-reader:1.1.2'
}
```

2. Add the barcode reader fragment to your activity
```xml
<fragment
        android:id="@+id/barcode_fragment"
        android:name="info.androidhive.barcode.BarcodeReader"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:auto_focus="true"
        app:use_flash="false" />
```

3. Implement your activity from <code>BarcodeReader.BarcodeReaderListener</code> and override the necessary methods.
```java
public class MainActivity extends AppCompatActivity implements BarcodeReader.BarcodeReaderListener {

    private BarcodeReader barcodeReader;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        barcodeReader = (BarcodeReader) getSupportFragmentManager().findFragmentById(R.id.barcode_fragment);
    }


    @Override
    public void onScanned(Barcode barcode) {
        // play beep sound
        barcodeReader.playBeep();
    }

    @Override
    public void onScannedMultiple(List<Barcode> list) {

    }

    @Override
    public void onBitmapScanned(SparseArray<Barcode> sparseArray) {

    }

    @Override
    public void onScanError(String s) {

    }
}
```

Adding Scanner Overlay Scanning Indicator
----
The overlay animation indicator displays a horizontal line animating from top to bottom. This will be useful to  to show some cool animation to indicate scanning progress.

To use it, add the <code>info.androidhive.barcode.ScannerOverlay</code> on top of barcode reader fragment using Relative or Frame layout.
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout ...>

    <fragment
        android:id="@+id/barcode_fragment"
        android:name="info.androidhive.barcode.BarcodeReader"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:auto_focus="true"
        app:use_flash="false" />

    <info.androidhive.barcode.ScannerOverlay
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="#44000000"
        app:line_color="#7323DC"
        app:line_speed="6"
        app:line_width="4"
        app:square_height="200"
        app:square_width="200"/>

</RelativeLayout>

```


Additional Options
-------------
XML attribute for **Barcode Reader**

<code>auto_focus</code> - boolean, turn on/off auto focus. Default is <code>true</code>

<code>use_flash</code> - boolean, turn on/off flash. Default is <code>false</code>


XML attribute for **Scanner Overlay** Indicator

<code>square_width</code> - Width of transparent square

<code>square_height</code> - Height of transparent square

<code>line_color</code> - Horizontal line color

<code>line_speed</code> - Horizontal line animation speed

----

JAVA Methods

- **Play beep sound**

You can play the **beep** sound when the barcode is scanned. This code is usually called in <code>onScanned()</code> callback.
```java
@Override
    public void onScanned(final Barcode barcode) {
        Log.e(TAG, "onScanned: " + barcode.displayValue);
        barcodeReader.playBeep();
        });
    }
```

- **Change beep sound**

You can change the default **beep** sound by passing the file name. You beep file should be in project's **assets** folder.
```java
barcodeReader.setBeepSoundFile("shutter.mp3");
```

- **Pause scanning**

The scanning can be paused by calling <code>pauseScanning()</code> method.
```java
barcodeReader.pauseScanning();
```

- **Resume Scanning**

The scanning can be resumed by calling <code>resumeScanning()</code> method.
```java
barcodeReader.resumeScanning();
```


## License
    Copyright (c) 2017 Ravi Tamada

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
