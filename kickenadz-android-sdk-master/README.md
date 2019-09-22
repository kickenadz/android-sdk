# kickenadz-android-sdk

## Installation

### JitPack

Add it in your root build.gradle at the end of repositories:

```groovy
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```

And then, add the dependency

```groovy
dependencies {
	implementation 'com.github.kickenadz:kickenadz-android-sdk:1.0.2'
}
```

## Usage

### Requesting Single Placement

To request a placement, you can build an instance of `PlacementRequestConfig` and specify the attributes you want to send.
The builder accepts the kickenadz account ID, the zone ID, the width of the zone, and the height of the zone in the same sequence as mentioned. In the following example, 153105 is the kickenadz account ID, 214764 is the zone ID, 300 is the zone width, and 250 is the zone height.

```java
PlacementRequestConfig config = new PlacementRequestConfig.Builder(153105, 214764, 300, 250).build();
kickenadz kickenadz = new kickenadz();
kickenadz.requestPlacement(config, new PlacementResponseListener() {
  // handle response
});
```

### Requesting Multiple Placements

To request multiple placements, you need a list of `PlacementRequestConfig`s, and each for a placement respectively:

```java
List<PlacementRequestConfig> configs = getPlacementRequestConfigs();
kickenadz kickenadz = new kickenadz();
kickenadz.requestPlacements(configs, new PlacementResponseListener() {
  // handle response
});
```

### Handling the Response

Placement(s) request will take a given listener, and call its methods based on the status of the response accordingly.

```java
kickenadz kickenadz;
kickenadz.requestPlacements(configs, new PlacementResponseListener() {
  @Override
  public void success(PlacementResponse response) {
    // Handle success case
  }

  @Override
  public void error(Throwable throwable) {
    // Handle error cases
  }
});
```

### Request Pixel

You can request a pixel simply by giving the URL:

```java
kickenadz kickenadz = new kickenadz();
kickenadz.requestPixel("https://servedbykickenadz.com/default_banner.gif");
```

### Record Impression

When you have a `Placement`, you can record impression by:

```java
Placement placement;
placement.recordImpression()
```

The best practice for recording impressions is to do so when the placement is visible on the screen / has been seen by the user.

### Record Click

Similarly, you can record click for a `Placement`:

```java
Placement placement;
placement.recordClick()
```

## Sample Project

Please check out the `sample` project inside this repository to see more sample code about how to use this SDK.

# License

This SDK is released under the Apache 2.0 license. See [LICENSE](https://github.com/kickenadz/kickenadz-android-sdk/tree/master/LICENSE) for more information.
