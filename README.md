# [Detox](https://github.com/wix/Detox) Helper for [CodeceptJS](https://codecept.io)

Testing Mobile Apps on iOS and Android can look like this:

```js
I.setLandscapeOrientation();
I.fillField('#text', 'a new text');
I.see('a new text', '#textValue');
I.dontSeeElement('#createdAndVisibleText');
I.click({ ios: '#GoButton', android: 'Button' });
I.waitForElement('#createdAndVisibleText', 20);
I.seeElement('#createdAndVisibleText');
I.runOnAndroid(() => {
  I.click('Save');
  I.see('Text Saved', '#message');
});
I.runOnIOS(() => {
  I.click('SAVE');
  I.see('SAVED!');
});
```

CodeceptJS provides next features over standard Detox:

- **Unified API**. The same test can be executed in Appium or Detox. Unified API helps different teams to use the same syntax and easy port tests from one engine to another.
- **Interactive pause**. When starting/stopping an application takes a long time, debugging and writing tests can be hard. 
CodeceptJS solves this by pausing an execution and letting you try different commands and locators. With this feature a test can be writtern during one running session.
- **One Test For Android and IOS**. When application differs on Android and IOS you can provide corresponding system-related locators for both systems. When needed a different code can be executed for Android and IOS keeping it inside the same test.


## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [Detox](#detox)
    -   [Setup](#setup)
    -   [Configuration](#configuration)
    -   [Parameters](#parameters)
    -   [relaunchApp](#relaunchapp)
    -   [launchApp](#launchapp)
    -   [installApp](#installapp)
    -   [shakeDevice](#shakedevice)
    -   [goBack](#goback)
    -   [setLandscapeOrientation](#setlandscapeorientation)
    -   [setPortraitOrientation](#setportraitorientation)
    -   [runOnIOS](#runonios)
        -   [Parameters](#parameters-1)
    -   [runOnAndroid](#runonandroid)
        -   [Parameters](#parameters-2)
    -   [tap](#tap)
        -   [Parameters](#parameters-3)
    -   [multiTap](#multitap)
        -   [Parameters](#parameters-4)
    -   [longPress](#longpress)
        -   [Parameters](#parameters-5)
    -   [click](#click)
        -   [Parameters](#parameters-6)
    -   [clickAtPoint](#clickatpoint)
        -   [Parameters](#parameters-7)
    -   [see](#see)
        -   [Parameters](#parameters-8)
    -   [dontSee](#dontsee)
        -   [Parameters](#parameters-9)
    -   [seeElement](#seeelement)
        -   [Parameters](#parameters-10)
    -   [dontSeeElement](#dontseeelement)
        -   [Parameters](#parameters-11)
    -   [seeElementExists](#seeelementexists)
        -   [Parameters](#parameters-12)
    -   [dontSeeElementExists](#dontseeelementexists)
        -   [Parameters](#parameters-13)
    -   [fillField](#fillfield)
        -   [Parameters](#parameters-14)
    -   [clearField](#clearfield)
        -   [Parameters](#parameters-15)
    -   [appendField](#appendfield)
        -   [Parameters](#parameters-16)
    -   [scrollUp](#scrollup)
        -   [Parameters](#parameters-17)
    -   [scrollDown](#scrolldown)
        -   [Parameters](#parameters-18)
    -   [scrollLeft](#scrollleft)
        -   [Parameters](#parameters-19)
    -   [scrollRight](#scrollright)
        -   [Parameters](#parameters-20)
    -   [swipeUp](#swipeup)
        -   [Parameters](#parameters-21)
    -   [swipeDown](#swipedown)
        -   [Parameters](#parameters-22)
    -   [swipeLeft](#swipeleft)
        -   [Parameters](#parameters-23)
    -   [swipeRight](#swiperight)
        -   [Parameters](#parameters-24)
    -   [wait](#wait)
        -   [Parameters](#parameters-25)
    -   [waitForElement](#waitforelement)
        -   [Parameters](#parameters-26)
    -   [waitForElementVisible](#waitforelementvisible)
        -   [Parameters](#parameters-27)
    -   [waitToHide](#waittohide)
        -   [Parameters](#parameters-28)

### Detox

**Extends Helper**

This is a wrapper on top of [Detox](https://github.com/wix/Detox) library by Wix aimied to unify testing experience for CodeceptJS framework.
Detox provides a grey box testing for mobile applications, playing especially good for React Native apps.

Detox plays quite differently from Appium. To establish detox testing you need to build a mobile application in a special way to inject Detox code.
This why Detox is grey box testing, so you need an access to application source code, and a way to build and execute it on emulator.

Comparing to Appium, Detox runs faster and more stable but requires an additional setup for build.

#### Setup

To install and condifure Detox [see the official guide for iOS](https://github.com/wix/Detox/blob/master/docs/Introduction.GettingStarted.md) and [Android](https://github.com/wix/Detox/blob/master/docs/Introduction.Android.md)

After you performed all steps required to set up Detox by itself you are ready to configure this helper. Install it via npm:

    npm i @codeceptjs/detox-helper --save

Detox configuration is required in `package.json` under `detox` section.

Example:

```js
 "detox": {
   "configurations": {
     "ios.sim.debug": {
       "binaryPath": "ios/build/Build/Products/Debug-iphonesimulator/example.app",
       "build": "xcodebuild -project ios/example.xcodeproj -scheme example -configuration Debug -sdk iphonesimulator -derivedDataPath ios/build",
       "type": "ios.simulator",
       "name": "iPhone 7"
     }
   }
 }
```

#### Configuration

In `codecept.conf.js` enable Detox helper:

```js
helpers: {
   Detox: {
     require: '@codeceptjs/detox',
     configuration: 'ios.sim.debug',
   }   
}
```

It's important to specify a package name under `require` section and current detox configuration taken from `package.json`.

Options:

-   `configuration` - a detox configuration name. Required.
-   `reloadReactNative` - should be enabled for React Native applications.

#### Parameters

-   `config`  

#### relaunchApp

Relaunches an application.

```js
I.relaunchApp();
```

#### launchApp

Launches an application. If application instance already exists, use [relaunchApp](#relaunchApp).

```js
I.launchApp();
```

#### installApp

Installs a configured application.
Application is installed by default.

```js
I.installApp();
```

#### shakeDevice

Shakes the device.

```js
I.shakeDevice();
```

#### goBack

Goes back on Android

```js
I.goBack(); // on Android only
```

#### setLandscapeOrientation

Switches device to landscape orientation

```js
I.setLandscapeOrientation();
```

#### setPortraitOrientation

Switches device to portrait orientation

```js
I.setPortraitOrientation();
```

#### runOnIOS

Execute code only on iOS

```js
I.runOnIOS(() => {
   I.click('Button');
   I.see('Hi, IOS');
});
```

##### Parameters

-   `fn`  a function which will be executed on iOS

#### runOnAndroid

Execute code only on Android

```js
I.runOnAndroid(() => {
   I.click('Button');
   I.see('Hi, Android');
});
```

##### Parameters

-   `fn`  a function which will be executed on android

#### tap

Taps on an element. 
Element can be located by its text or id or accessibility id.

The second parameter is a context element to narrow the search.

Same as [click](#click)

```js
I.tap('Login'); // locate by text
I.tap('~nav-1'); // locate by accessibility label
I.tap('#user'); // locate by id
I.tap('Login', '#nav'); // locate by text inside #nav
I.tap({ ios: 'Save', android: 'SAVE' }, '#main'); // different texts on iOS and Android
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))**  (optional, default `null`)

#### multiTap

Multi taps on an element.
Element can be located by its text or id or accessibility id.

Set the number of taps in second argument.
Optionally define the context element by third argument.

```js
I.multiTap('Login', 2); // locate by text
I.multiTap('~nav', 2); // locate by accessibility label
I.multiTap('#user', 2); // locate by id
I.multiTap('Update', 2, '#menu'); // locate by id
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `num` **int** number of taps
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### longPress

Taps an element and holds for a requested time.

```js
I.longPress('Login', 2); // locate by text, hold for 2 seconds
I.longPress('~nav', 1); // locate by accessibility label, hold for second
I.longPress('Update', 2, '#menu'); // locate by text inside #menu, hold for 2 seconds
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `sec` **num** number of seconds to hold tap
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### click

Clicks on an element. 
Element can be located by its text or id or accessibility id

The second parameter is a context (id | type | accessibility id) to narrow the search.

Same as [tap](#tap)

```js
I.click('Login'); // locate by text
I.click('~nav-1'); // locate by accessibility label
I.click('#user'); // locate by id
I.click('Login', '#nav'); // locate by text inside #nav
I.click({ ios: 'Save', android: 'SAVE' }, '#main'); // different texts on iOS and Android
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))**  (optional, default `null`)

#### clickAtPoint

Performs click on element with horizontal and vertical offset.
An element is located by text, id, accessibility id.

```js
I.clickAtPoint('Save', 10, 10);
I.clickAtPoint('~save', 10, 10); // locate by accessibility id
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 
-   `x` **int** horizontal offset (optional, default `0`)
-   `y` **int** vertical offset (optional, default `0`)

#### see

Checks text to be visible.
Use second parameter to narrow down the search.

```js
I.see('Record created');
I.see('Record updated', '#message');
I.see('Record deleted', '~message');
```

##### Parameters

-   `text` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** to check visibility
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element inside which to search for text (optional, default `null`)

#### dontSee

Checks text not to be visible.
Use second parameter to narrow down the search.

```js
I.dontSee('Record created');
I.dontSee('Record updated', '#message');
I.dontSee('Record deleted', '~message');
```

##### Parameters

-   `text` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** to check invisibility
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element in which to search for text (optional, default `null`)

#### seeElement

Checks for visibility of an element.
Use second parameter to narrow down the search.

```js
I.seeElement('~edit'); // located by accessibility id
I.seeElement('~edit', '#menu'); // element inside #menu
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### dontSeeElement

Checks that element is not visible.
Use second parameter to narrow down the search.

```js
I.dontSeeElement('~edit'); // located by accessibility id
I.dontSeeElement('~edit', '#menu'); // element inside #menu
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### seeElementExists

Checks for existence of an element. An element can be visible or not.
Use second parameter to narrow down the search.

```js
I.seeElementExists('~edit'); // located by accessibility id
I.seeElementExists('~edit', '#menu'); // element inside #menu
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### dontSeeElementExists

Checks that element not exists.
Use second parameter to narrow down the search.

```js
I.dontSeeElementExist('~edit'); // located by accessibility id
I.dontSeeElementExist('~edit', '#menu'); // element inside #menu
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element to locate
-   `context` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** context element (optional, default `null`)

#### fillField

Fills in text field in an app.
A field can be located by text, accessibility id, id.

```js
I.fillField('Username', 'davert');
I.fillField('~name', 'davert');
I.fillField({ android: 'NAME', ios: 'name' }, 'davert');
```

##### Parameters

-   `field` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an input element to fill in
-   `value` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to fill

#### clearField

Clears a text field.
A field can be located by text, accessibility id, id.

```js
I.clearField('~name');
```

##### Parameters

-   `field` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an input element to clear

#### appendField

Appends text into the field.
A field can be located by text, accessibility id, id.

```js
I.appendField('name', 'davert');
```

##### Parameters

-   `field` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 
-   `value` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

#### scrollUp

Scrolls to the top of an element.

```js
I.scrollUp('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 

#### scrollDown

Scrolls to the bottom of an element.

```js
I.scrollDown('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 

#### scrollLeft

Scrolls to the left of an element.

```js
I.scrollLeft('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 

#### scrollRight

Scrolls to the right of an element.

```js
I.scrollRight('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** 

#### swipeUp

Performs a swipe up inside an element.
Can be `slow` or `fast` swipe.

```js
I.swipeUp('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element on which to perform swipe
-   `speed` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a speed to perform: `slow` or `fast`. (optional, default `'slow'`)

#### swipeDown

Performs a swipe up inside an element.
Can be `slow` or `fast` swipe.

```js
I.swipeUp('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element on which to perform swipe
-   `speed` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a speed to perform: `slow` or `fast`. (optional, default `'slow'`)

#### swipeLeft

Performs a swipe up inside an element.
Can be `slow` or `fast` swipe.

```js
I.swipeUp('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element on which to perform swipe
-   `speed` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a speed to perform: `slow` or `fast`. (optional, default `'slow'`)

#### swipeRight

Performs a swipe up inside an element.
Can be `slow` or `fast` swipe.

```js
I.swipeUp('#container');
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element on which to perform swipe
-   `speed` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a speed to perform: `slow` or `fast`. (optional, default `'slow'`)

#### wait

Waits for number of seconds

```js
I.wait(2); // waits for 2 seconds
```

##### Parameters

-   `sec` **int** number of seconds to wait

#### waitForElement

Waits for an element to exist on page.

```js
I.waitForElement('#message', 1); // wait for 1 second
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element to wait for
-   `sec` **int** number of seconds to wait, 5 by default (optional, default `5`)

#### waitForElementVisible

Waits for an element to be visible on page.

```js
I.waitForElementVisible('#message', 1); // wait for 1 second
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element to wait for
-   `sec` **int** number of seconds to wait (optional, default `5`)

#### waitToHide

Waits an elment to become not visible.

```js
I.waitToHide('#message', 2); // wait for 2 seconds
```

##### Parameters

-   `locator` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** an element to wait for
-   `sec` **int** number of seconds to wait (optional, default `5`)