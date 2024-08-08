# react-native-native-serialport

[![npm version](http://img.shields.io/npm/v/react-native-native-serialport.svg?style=flat-square)](https://npmjs.org/package/react-native-native-serialport "View this project on npm")
[![npm downloads](http://img.shields.io/npm/dm/react-native-native-serialport.svg?style=flat-square)](https://npmjs.org/package/react-native-native-serialport "View this project on npm")
[![npm licence](http://img.shields.io/npm/l/react-native-native-serialport.svg?style=flat-square)](https://npmjs.org/package/react-native-native-serialport "View this project on npm")
[![Platform](https://img.shields.io/badge/platform-android-989898.svg?style=flat-square)](https://npmjs.org/package/react-native-native-serialport "View this project on npm")

Native serial port for react-native on Android.

The native serial port lib use <https://github.com/licheedev/Android-SerialPort-API>.

For react-native USB serial port, please ref to <https://github.com/flyskywhy/react-native-usb-serialport>.

## Install
`npm install react-native-native-serialport`


Add `maven { url 'https://jitpack.io' }` into `build.gradle`:

```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

## Usage
```javascript
import RNSerialPort from 'react-native-native-serialport';
```

* get device path list
```javascript
RNSerialPort.getAllDevicesPath(result => console.log(result));
```

* open serial port
```javascript
RNSerialPort.openSerialPort('/dev/ttySO', 9600);
```

* send data
```javascript
let byteData = [0x00, 0x01, 0x02, 0x03, 0x05];
RNSerialPort.sendByteData('/dev/ttyS7', byteData);
```

* monitor status and data on serial port
```javascript
const emitter = Platform.OS === 'ios' ? {
    addListener: () => {},
    removeListener: () => {},
    emit: () => {},
} : DeviceEventEmitter;

emitter.addListener('onSerialPortRecevieData', this.onSerialPortRecevieData);
emitter.addListener('onSerialPortOpenStatus', this.onSerialPortOpenStatus);

onSerialPortOpenStatus(status) {
    console.log("onSerialPortOpenStatus");
    console.log(status);
}

onSerialPortRecevieData(data) {
    console.log("onSerialPortRecevieData");
    console.log(data);
}
```

And can ref to `example/RNSerialPortManager.js`.
