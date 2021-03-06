# Optimizely Cordova Plugin

iOS Build [![Build Status](https://travis-ci.org/optimizely/optimizely-cordova-plugin.svg?branch=master)](https://travis-ci.org/optimizely/optimizely-cordova-plugin)

Android Build [![Circle CI](https://circleci.com/gh/optimizely/optimizely-cordova-plugin/tree/master.svg?style=svg)](https://circleci.com/gh/optimizely/optimizely-cordova-plugin/tree/master)

Cordova Plugin for the Optimizely iOS and Android SDKs

Allows developers developing hybrids apps using Cordova platforms such as Phonegap, Crosswalk, Ionic, Intel XDK to use the Optimizely SDKs for A/B
testing and beyond!

- [Android SDK Version 1.4.1](http://developers.optimizely.com/android/changelog/index.html#\31 -4-1)
- [iOS SDK Version 1.4.0](http://developers.optimizely.com/ios/changelog/index.html#\31 -4-0)

## Table of Contents
1. [Usage](#usage)
2. [Available Features](#available-features)
  1. [Live Variables](#live-variables)
  2. [Code Blocks](#code-blocks)
3. [APIs](#apis)


## Installation

### Edge

`cordova plugin add https://github.com/optimizely/optimizely-cordova-plugin`

### Stable (via npm)

`cordova plugin add cordova-plugin-optimizely`


## Uninstall plugin

Use the cordova CLI to remove the plugin

`cordova plugin remove cordova-plugin-optimizely`


## Start A/B Testing!

1. If you haven't already, sign up for an account at [Optimizely](www.optimizely.com/mobile)

2. Create a Android or iOS project

3. Grab your project token

4. Register [Live Variables](#live-variables) and [Code Blocks](#code-blocks)

5. Call startOptimizely with your token
```
window.optimizely.startOptimizely(<token>)
  .then(
    function(result) {
      // success callback
    },
    function(error) {
      // error callback
    }
  )
```

## Available Features
The optimizely cordova plugin allows cordova based apps to use the Live Variable and Code Block features of the Optimizely Mobile SDKs. Visual experiments are currently not supported.

### 1. Live Variables
Live Variables allow you to designate variables in your app that can be assigned values in the Optimizely editor. These values can be modified by Optimizely's editor even after you have released your app to the app store. For example, you might want to create an experiment that tests various values for gravity.

To register a live variable you can call the Optimizely API:
```
window.optimizely.numberVariable('gravity', 9.8)
  .then(
    function() {
      // this callback function will execute once the variable has been registered with the Optimizely SDK
    },
    function(errorMsg) {
     // error callback
    }
  );
```

To use the live variable:
```
window.optimizely.numberForKey('gravity')
  .then(
    function(variableValue) {
      // this callback function will execute once the plugin has retrieved the stored value for the given variable key.
    },
    function(errorMsg) {
      // error callback
    }
  );
```

### 2. Code Blocks
Code Blocks allow developers to create variations that execute different code paths. For example, one use case might be to test various checkout flows.

To register a code block:
```
window.optimizely.codeBlock('checkoutFlow', ['single_page', 'multi_page'])
  .then(
    function() {
      // success callback
    },
    function(errorMsg) {
      // error callback
    }
  );
```

To use a code block:
```
window.optimizely.executeCodeBlock(
  'checkoutFlow',
  [
    function() {
      // single page checkout flow
    },
    function() {
      // multi page checkout flow
    }
  ],
  this,
  function(errorMsg) {
    // error callback
  }
)
```

## APIs
Aside from the APIs for registering and using Live Variables and Code Blocks, the plugin also exposes the following APIs:
- `window.optimizely.enabledEditor()`
- `window.optimizely.refreshExperimentData()`
- `window.optimizely.setCustomTag(tagName, tagValue)`
- `window.optimizely.startOptimizely(projectToken)`
- `window.optimizely.trackEvent('eventName')`
- `window.optimizely.trackRevenueWithDescription(100, 'revenueDescription')`

All API calls return a Promise object using the ES6 promise specification.

For more information on these APIs please visit [Android Docs](http://developers.optimizely.com/android/reference/index.html) or [iOS Docs](http://developers.optimizely.com/ios/reference/index.html)

More documentation coming soon!
