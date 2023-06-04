

# CHANGES:

- packaging option error [fix](https://stackoverflow.com/questions/44954122/more-than-one-file-was-found-with-os-independent-path-lib-x86-libusb-so)
- react native build [fix](https://github.com/facebook/react-native/issues/35210#issuecomment-1304536693)
    

## Steps:

In `example` folder execute:

`npm install`

`export NODE_OPTIONS=--openssl-legacy-provider`

because: https://stackoverflow.com/a/69699772/10478535

`react-native start`

In separate terminal window:

Run `adb devices` and get your device id

```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools

react-native run-android --deviceId=DEVICE_ID
```


## Env

jdk8-openjdk, java 1.8.0_372

npm 8.19.2

nodejs v20.2.0

## Useful links


React Native: 

https://reactnative.dev/docs/running-on-device

https://reactnative.dev/docs/environment-setup?package-manager=yarn&guide=native

Java on archlinux:

https://rtfm.co.ua/en/arch-linux-set-a-java-version/

https://wiki.archlinux.org/title/java

https://youtu.be/M70Xebbj4Qk

==========================================================================

# Original Readme


A [VisionCamera](https://github.com/mrousavy/react-native-vision-camera) Frame Processor Plugin to preform text detection on images using [**MLKit Vision** Text Recognition](https://developers.google.com/ml-kit/vision/text-recognition).

## Installation

```sh
yarn add vision-camera-ocr
cd ios && pod install
```

Add the plugin to your `babel.config.js`:

```js
module.exports = {
  plugins: [
    [
      'react-native-reanimated/plugin',
      {
        globals: ['__scanOCR'],
      },
    ],

    // ...
```

> Note: You have to restart metro-bundler for changes in the `babel.config.js` file to take effect.

## Usage

```js
import { labelImage } from "vision-camera-image-labeler";

// ...
const frameProcessor = useFrameProcessor((frame) => {
  'worklet';
  const scannedOcr = scanOCR(frame);
}, []);
```

## Data

`scanOCR(frame)` returns an `OCRFrame` with the following data shape. See the example for how to use this in your app.

 ``` jsx
  OCRFrame = {
    result: {
      text: string, // Raw result text
      blocks: Block[], // Each recognized element broken into blocks
    ;
};
```

The text object closely resembles the object documented in the MLKit documents.
https://developers.google.com/ml-kit/vision/text-recognition#text_structure

```
The Text Recognizer segments text into blocks, lines, and elements. Roughly speaking:

a Block is a contiguous set of text lines, such as a paragraph or column,

a Line is a contiguous set of words on the same axis, and

an Element is a contiguous set of alphanumeric characters ("word") on the same axis in most Latin languages, or a character in others
```



## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the development workflow.

## License

MIT
