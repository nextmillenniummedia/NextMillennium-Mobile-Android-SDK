# NextMillennium Android SDK Intergration Guide
We are happy to announce the release of NextMillennium Android SDK for Mobile Ads. 
 

###  Change history


|        Version        |Release date                          |Description                         |
|----------------|-------------------------------|-----------------------------|
|1.0.0|november 2020          |• initial release.           |
|1.0.1          |january 2021            |??????           |

### GMA SDK Compatibility Matrix

|NM SDK Version |GMS play-services-ads Version                         |Repository                         |
|----------------|-------------------------------|-----------------------------|
|1.0.1 |18.2.0         |jcenter() ?????          |


###  Key features

####  Modes of ad display

You can choose which ad display mode is preferrable to you: Classic or Injection.
 
| Type  | Description                         |                   
|----------------|-------------------------------|
|**Classic** |choose exact place where you want to display NextMillennium mobile ads in your app |   
|**Injection** |manage your ads dynamically: turn them on/off, choose at which activities you want to display ads and see result in a few seconds, you don t need to reinstall the SDK to change the position of an ad.   |

# Installation

### Through Gradle
```gradle
repositories {
  // your repos
  maven { url 'https://sdk.brainlyads.com/android/repository' }
}
```
```gradle
dependencies {
  implementation 'com.nextmillenium:inappsdk:1.0.0-beta01'
}
```
### Through aar file

Add to build.gradle at project level into repositories block the repository:

```repositories {
flatDir { dirs 'libs'}
}
```

Add dependency to build.gradle block:

```dependencies {
implementation(name: 'inappsdk', ext: 'aar')
}
```


# Initialization
## Add API key

Get API keys and add them to application manifest file.

```gradle
<meta-data
      android:name="com.nextmillenium.inappsdk.API_KEY"
      android:value="[NEXTMILLENNIUM_MOBILE_ADS_API_KEY_HERE]"/>
<meta-data
       android:name="com.google.android.gms.ads.APPLICATION_ID"
       android:value="[PUT_API_KEY_HERE]"/>
}
```



Call ```InAppSdk.initialize(this)``` method in application class in onCreate method.


## Send Activities
In Application class in onCreate() method, add the following code to send the list of activities. Call this method only once when you install the SDK into your app. It should be also called when the list of activities has been changed. 

```
override fun onCreate() {
  if (BuildConfig.DEBUG) {
    InAppSdk.sendScreenNames(this)
  }
```
  
In Activity class in onCreate() method add:

```
override fun onCreate(savedinstancestate: Bundle?) {
  inappsdk.inject(this)
}
```

## Initialize Ad display

To initialize the load of banners into recyclerView list or into TextView list you need to wrap recyclerView or TextView into ```InContentView```.

RecyclerView example:

    <com.nextmillenium.inappsdk.core.ui.InContentView
    android:id="@+id/inContentView"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recyclerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
    
    </com.nextmillenium.inappsdk.core.ui.InContentView>

TextView example:

    <com.nextmillenium.inappsdk.core.ui.InContentView
    android:id="@+id/inContentView"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
    android:id="@+id/textView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
    
    </com.nextmillenium.inappsdk.core.ui.InContentView>

Find views: 

```InContentView inContentView = findViewById(R.id.inContentView);```

The last step is to call the following methods in Activity class.

RecyclerView example:

```incontentView.setContent()``` // As a parameter for this method use  recyclerView.adapter 
// after this call
```inAppSdk.inject(this)```

TextView example: 

```inContentView.setContent(“text”)``` // after this call ```inAppSdk.inject(this)```




