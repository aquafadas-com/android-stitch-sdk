# Stitch

This document targets stitch SDK users.

The Stitch SDK allow to create dynamic kiosk, configurable from Stitch Editor.
On the Stitch Editor, the user can update widgets contained in the Stitch with widget like banners, videos.

## This page covers:

*   [Requirements](#Requirements)
*   [Getting started](#Setup)
*   [Next Step](#nextStep)
*   [Changelog](#Changelog)

## <a name="Requirements"></a> Requirements
### Supported Android Versions

The library works with any `minSdkVersion` greater than or equal to `16`.

The targeted android version is '28'.

You need to have an app in an implementation of Stitch editor.


## <a name="Setup"></a> Getting Started
### #1 Add dependency to your app's build.gradle`
In order to build a **Stitch** application, you will have to add the android Rakuten Aquafadas SDK dependency.

The Aquafadas SDK libraries are located under the rakuten artifactory repository.

You can add it inside your build.gradle's repositories dependencies with the following code.

```groovy
repositories {
    maven {url 'http://artifactory.raksdtd.com/artifactory/libs-release'}
}

dependencies {
...
    implementation 'com.aquafadas:stitch:[version]'
...
}
```

### #2 Configure Mission control app id in `AndroidManifest.xml`
You must provide Configuration the [app id](https://developers.rakuten.com/intra/mission-control/guides/getting-started/guide-to-get-app-id/)
as metadata in application manifest file to connect your app to Mission control.

```xml
<manifest>
    <application>
        <meta-data android:name="com.rakuten.tech.mobile.relay.AppId"
                   android:value="[appid]" />
    </application>
</manifest>
```


### #3 Launch the Stitch Activity
To launch a Stitch view , just open the activity `StitchActivity`.

You can add a `Stitch id` and the `language` in the intent's extras to launch a specific Stitch. 
If no extras are added, the Stitch Activity will automatically load the default Stitch View of the app. 

```java
Intent stitchIntent = new Intent([context], StitchActivity.class);
stitchIntent.putExtra(StitchActivity.STITCH_ID_EXTRA, [Stitch id]);
stitchIntent.putExtra(StitchActivity.STITCH_LANGUAGE_EXTRA, [Stitch language]);
startActivity(stitchIntent);
```

## <a name="nextStep"></a> Next step 

### Configuration
The stitch SDK is configured via manifest meta-data, the configurable values are:

| Field                          | Datatype| Manifest Key                                               | Optional   |
|--------------------------------|---------|------------------------------------------------------------|------------|
| Mission control application ID | string  | `com.rakuten.tech.mobile.relay.AppId`                      | ❌         |

<details>
<summary>Full Examlpe (click to expand)</summary>

```xml
<manifest>
  <application >
    <!--Mandatory meta data-->
    <meta-data
      android:name="com.rakuten.tech.mobile.relay.AppId"
      android:value="[your app Id]"/>
  </application>
</manifest>
```
</details>


It's also possible to configure end points by overriding string resources, the configurable values are:

| Resource                       | Datatype| Manifest Key                                   |Default value                                                                                   |
|--------------------------------|---------|------------------------------------------------|------------------------------------------------------------------------------------------------|
| Kyashu api end point           | string  | `stitch_kyashu_end_point`                      |https://api-kyashu.aquafadas.com/wsapi/KyashuDownload.php?service=KS-AvePublishing              |
| Stitch api end point           | string  | `stitch_api_end_point`                         |https://api-stitch.aquafadas.com                                                                |

<details>
<summary> Example for targetting staging environment (click to expand)</summary>

```xml
<resources>
  <string name="stitch_kyashu_end_point">[your Kyashu Url end point]</string>
  <string name="stitch_api_end_point">[your Stitch api end point]</string>
</resources>
```
</details>

### Launch a Stitch Fragment

A Stitch view is a fragment, named `StitchFragment`.
This fragment can be added to a layout.

First, add a container for the fragment.

```xml
  <FrameLayout
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
  </FrameLayout>
```

Then add the fragment.

```java
StitchFragment stitchFragment = StitchFragment.newInstance([Sitch id], [Stitch Language]);

getSupportFragmentManager().beginTransaction()
    .replace(R.id.container, stitchFragment, "stitch-" + stitchId)
    .commit();
```

To handle navigation between Stitches, your activity needs to implement the interface `StitchDefaultActionListener`.

```java
@Override
public void process(StitchWidgetInterface widget) {
  if (widget != null) {
    String reference = widget.getReference();
    if (reference != null && !reference.isEmpty() && widget.getType() == StitchWidgetType.stitchView) {

      StitchFragment newStitchFragment = StitchFragment.newInstance(reference, [Stitch language]);

      getSupportFragmentManager().beginTransaction()
          .replace(R.id.container, newStitchFragment, "stitch-" + reference)
          .addToBackStack(null)
          .commit();
    }
  }
}
```

To get notified every time a stitch is loaded, implement in your activity the interface `StitchLoadedListener`

You can get an exemple for the implementation of the `StitchFragment` in the Sample app, activity `StitchFragmentSampleActivity`.
