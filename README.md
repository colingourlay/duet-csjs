# duet-csjs

Use [CSJS](https://github.com/rtsao/csjs) with [duet](https://github.com/colingourlay/duet) by passing CSS Modules-enabled stylesheets from the worker thread to the main thread which are injected into the document's head.

```
$ npm install duet-csjs
```

## Usage

```javascript
var duet    = require('duet');
var channel = require('duet-csjs/channel');
var csjs    = require('duet-csjs');

var GREY = '#ccc';
var GREEN = '#3c3';

var styles = csjs`
    .button {
        display: inline-block;
        border-radius: 5px;
        background-color: ${GREY};
    }

    .sucess-button extends .button {
        background-color: ${GREEN};
    }
`;

duet([channel], function () {
    // styles were queued and sent once duet connected the channel
});
```

## API

Please refer to the [CSJS documentation](https://github.com/rtsao/csjs/blob/master/README.md#quick-example). This plugin transparently wraps the existing API with a function that sends compiled styles from the worker thread to the main thread, where [insert-css](https://github.com/substack/insert-css) is used to insert them into the document's `<head>` as a `<style>` element.

## Example

An example can be seen in the [duet example app](https://github.com/colingourlay/duet-example-app).
