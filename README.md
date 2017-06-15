
# react-native-scandit

## Getting started

`$ npm install react-native-scandit@https://github.com/salathegroup/react-native-scandit.git --save`

### Mostly automatic installation

`$ react-native link react-native-scandit`

Notes:
- Scandit's SDK is required. See below how add it to iOS and Android projects)
- You might need to allow access to the camera, both for iOS and Android

### Manual installation


#### iOS

1. In Xcode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-scandit` and add `SGScandit.xcodeproj`
3. In Xcode, in the project navigator, select your project. Add `libSGScandit.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.reactlibrary.SGScanditPackage;` to the imports at the top of the file
  - Add `new SGScanditPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-scandit'
  	project(':react-native-scandit').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-scandit/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-scandit')
  	```


### Add Scandit SDK

#### iOS

1. Download Scandit SDK for iOS and uncompress the archive.
2. Add ScanditBarcodeScanner.framework to the iOS project in target build phase "Link Binary With Libraries".
3. Add libiconv.tbd and libz.tbd there too (needed by Scandit framework).
4. Add the path to the folder containing ScanditBarcodeScanner.framework in project's build settings (Search Paths / Framework Search Paths)

#### Android

1. Download Scandit SDK for Android and uncompress the archive.
2. Add the following to your project's app build.gradle (the file is in the ScanditSDK subfolder of the SDK):
  	```
  	repositories {
  	    flatDir{
  	        dirs '/PATH/TO/ScanditBarcodeScanner.aar'
  	    }
  	}
  	```


## Usage
```javascript
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, View, Text } from 'react-native';

import Scandit, { ScanditPicker, ScanditSDKVersion } from 'react-native-scandit';

Scandit.setAppKey('<YOUR SCANDIT APP KEY>');

export default class ex2 extends Component {
  render() {
    return (
      <View style={{ flex: 1 }}>
        <ScanditPicker
          ref={(scan) => { this.scanner = scan; }}
          style={{ flex: 1 }}
          settings={{
            enabledSymbologies: ['EAN13', 'EAN8', 'UPCE'],
            cameraFacingPreference: 'back'
          }}
          onCodeScan={(code) => {alert(code.data);}}
        />
      <Text>Using Scandit SDK {ScanditSDKVersion}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('MyFirstScanditApp', () => >MyFirstScanditApp);
```
