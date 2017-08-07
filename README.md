Barcode Reader - Google Mobile Vision
===================
Android Barcode Reader library using **Google Mobile Vision.** This library is built on top of google mobile vision sample adding improvements and fixing few bugs.

----------

Movie Tickets Sample App
-------------
Below app is built using this library adding few UI improvements to showcase the usefulness of the library.

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
XML attribute for Barcode Reader
```xml
<!-- turn on auto focus. default is true -->
<attr name="auto_focus" format="boolean" />

<!-- turn on flash. default is false -->
<attr name="use_flash" format="boolean" />
```
XML attribute for **Scanner Overlay** Indicator
```xml
<!-- transparent square width / height -->
<attr name="square_width" format="integer" />
<attr name="square_height" format="integer" />

<!-- horizontal line color -->
<attr name="line_color" format="color" />

<!-- horizontal line height -->
<attr name="line_width" format="integer" />

<!-- horizontal line animation speed. Use b/w (0 - 10) -->
<attr name="line_speed" format="integer" />
```

JAVA Methods

- Play beep sound
You can play the **beep** sound when the barcode is scanned. This code is usually called in <code>onScanned()</code> callback.
```java
@Override
    public void onScanned(final Barcode barcode) {
        Log.e(TAG, "onScanned: " + barcode.displayValue);
        barcodeReader.playBeep();
        });
    }
```

- Change beep sound
You can change the default **beep** sound by passing the file name. You beep file should be in project's **assets** folder.
```java
barcodeReader.setBeepSoundFile("shutter.mp3");
```
- Pause scanning
The scanning can be paused by calling <code>pauseScanning()</code> method.
```java
barcodeReader.pauseScanning();
```

- Change beep sound
The scanning can be resumed by calling <code>resumeScanning()</code> method.
```java
barcodeReader.resumeScanning();
```


JAVA methods
-Play Beep soun
You can turn on / off flash by calling 
- Auto Focus


Features
-------------
> Scans barcode / QR code from the camera stream
> You can add camera overlay scan horizontal line animation

StackEdit stores your documents in your browser, which means all your documents are automatically saved locally and are accessible **offline!**

> **Note:**

> - StackEdit is accessible offline after the application has been loaded for the first time.
> - Your local documents are not shared between different browsers or computers.
> - Clearing your browser's data may **delete all your local documents!** Make sure your documents are synchronized with **Google Drive** or **Dropbox** (check out the [<i class="icon-refresh"></i> Synchronization](#synchronization) section).
