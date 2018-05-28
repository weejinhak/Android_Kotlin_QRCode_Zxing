# Android QR Code Zxing Library 

* app level에서 build.gradle에 추가

```groovy
 //zxing
 implementation 'com.journeyapps:zxing-android-embedded:3.6.0'  
```

> Qr Code Read

* manifests

```groovy
 <uses-permission android:name="android.permission.CAMERA"/>
```

* Activity listener Event

```groovy
IntentIntegrator(this).initiateScan() // `this` is the current Activity
```

* Return result Method

```kotlin
    // QR Code Get the results
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent) {
        val result = IntentIntegrator.parseActivityResult(requestCode, resultCode, data)
        if (result != null) {
            if (result.contents == null) {
                Toast.makeText(this, "Cancelled", Toast.LENGTH_LONG).show()
            } else {
                Toast.makeText(this, "Scanned: " + result.contents, Toast.LENGTH_LONG).show()
            }
        } else {
            super.onActivityResult(requestCode, resultCode, data)
        }
    }
```

> Qr Code Write

* Qr Code Write Code

```kotlin
   val multiFormatWriter = MultiFormatWriter()
   val bitMatrix: BitMatrix = multiFormatWriter.encode("UserInputText", BarcodeFormat.QR_CODE, 200, 200)
   val barcodeEncoder = BarcodeEncoder()
   val bitmap: Bitmap = barcodeEncoder.createBitmap(bitMatrix)

   imageView.setImageBitmap(bitmap)
```