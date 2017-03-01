# SplashScreen
### The right way to do it...

**What Google Recommends**
You may be surprised to hear that Google advocates that you use a splash screen. It’s right [here](https://material.io/guidelines/patterns/launch-screens.html)in the material design specs.


**Implementing a Splash Screen**
Implementing a splash screen the right way is a little different than you might imagine. The splash view that you see has to be ready immediately, even before you can inflate a layout file in your splash activity.

So you will not use a layout file. Instead, specify your splash screen’s background as the activity’s theme background. To do this, first create an XML drawable in res/drawable.

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
	<item
		android:drawable="@drawable/bgd_gradient"/>
	<item>
		<bitmap android:src="@drawable/your_logo_here"
		        android:gravity="center"
			/>
	</item>
</layer-list>
```

Here, I’ve set up a background gradient and an image.
The background gradient is created with a drawable shape through the new XML file `bgd_gradient.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:shape="rectangle">
	<gradient
		android:angle="90"
		android:centerColor="#FFBBBBBB"
		android:centerX="38%"
		android:endColor="#FF808080"
		android:startColor="#FF808080"
		android:type="linear"/>
</shape>
```

Next, you will set this as your splash activity’s background in the theme. Navigate to your styles.xml file and add a new theme for your splash activity:

```xml
<resources>
	<!-- Base application theme. -->
	<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
		<!-- Customize your theme here. -->
		<item name="colorPrimary">@color/colorPrimary</item>
		<item name="colorPrimaryDark">@color/colorPrimaryDark</item>
		<item name="colorAccent">@color/colorAccent</item>
	</style>
	<style name="SplashScreen" parent="Theme.AppCompat.Light.NoActionBar">
		<item name="android:windowBackground">@drawable/bgd_splash_screen</item>
	</style>
</resources>
```

Configure this as your splash activity’s theme in your AndroidManifest.xml:

```xml
(...)
<activity
	android:name=".SplashScreenActivity"
	android:theme="@style/SplashScreen">
	<intent-filter>
		<action android:name="android.intent.action.MAIN"/>

		<category android:name="android.intent.category.LAUNCHER"/>
	</intent-filter>
</activity>
<activity android:name=".MainActivity">
</activity>
(...)
```

Finally, your SplashActivity class should just forward you along to your main activity:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);

	Intent intent = new Intent(this, MainActivity.class);
	startActivity(intent);
	finish();
}
```

Notice that you don’t even set up a view for this SplashActivity. The view comes from the theme. When you set up the UI for your splash activity in the theme, it is available immediately.

![alt text](https://github.com/micaelc/android-spashscreen/art/SpalshScreen.png)