# react-native-jarvis-mobile-location-gateway-sdk

react native sdk for mobile to be acted as gateway

## Installation

```sh
npm install react-native-jarvis-mobile-location-gateway-sdk
```

```sh
yarn add react-native-jarvis-mobile-location-gateway-sdk
```
#### Auto linking when using React Native >= 0.60

## Setup

#### For Android

1. Register permission and services in `AndroidManifest.xml`
```js
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.jarvisappsdktest">

  <!-- Require android phone supports Bluetooth Low Energy -->
  <uses-feature
    android:name="android.hardware.bluetooth_le"
    android:required="true" />

  <!-- Required permissions -->
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
  <uses-permission android:name="android.permission.BLUETOOTH" />
  <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
  <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />

  <application
    android:name=".MainApplication">
    <!-- Your code -->

    <!-- Register SDK service here -->
    <service
      android:name="com.jarvis.reactnative.mobilegateway.services.BleScannerService"
      android:exported="false"
      android:foregroundServiceType="location|dataSync" />
  </application>
</manifest>
```

#### 2. Request permissions in your app
Please make sure the following permission is allowed before start using our Sdk.

`BLUETOOTH_SCAN`

`ACCESS_FINE_LOCATION`

`ACCESS_COARSE_LOCATION`

`ACCESS_BACKGROUND_LOCATION`

## Usage

```ts
import {
  startLocating,
  stopLocating,
  registerCallback,
  unregisterCallback
} from 'react-native-jarvis-mobile-location-gateway-sdk';

// this sdk key is required to start sdk
const sdkKey = `please_get_this_from_jarvis`;

// only start the sdk when all permissions allowed
const onAllPermissionAllowed = async () : Promise<void> => {
  // start the sdk
  registerCallback(onFound, onLeave);

  const range = 10; // configure the distance filter, unit: meter
  const result = await startLocating(sdkKey, range);

  if (!result.errorCode) {
    console.log("Start Successfully!");
  }
};

const onFound = (mac: string, userId: string, lat: number, lng: number, distanceToTheGateway: number) : void => {
  // handle your logic here
};

const onLeave = (mac: string, userId: string) : void => {
  // handle your logic here
};
```

## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the development workflow.

## License

MIT

---

Made with [create-react-native-library](https://github.com/callstack/react-native-builder-bob)
