---
id: taiko-check-page
sidebar_position: 1
title: Check page is alive
---

# Check that a content page is alive

## Plan
From the Taiko recorder, visit `https://cxharris.github.io/docs` and wait for the test to pass or fail. The *waiting* is performed implicitly by Taiko. 

## Implementation

In the Taiko recorder, type:

```
> openBrowser()
> goto("https://cxharris.github.io/docs")
>
```
Taiko will command the open browser to visit the specified page.

### Generated code
```
const { openBrowser, goto, closeBrowser } = require('taiko');
(async () => {
    try {
        await openBrowser();
        await goto("https://cxharris.github.io/docs");
    } catch (error) {
        console.error(error);
    } finally {
        await closeBrowser();
    }
})();
```

## Results

Success looks like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs")
[PASS] Navigated to URL https://cxharris.github.io/docs
>
```
A failed visit would look like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs")
'[FAIL] Error: Navigation to url https://cxharris.github.io/docs failed.
' +
  ' STATUS: 404, STATUS_TEXT: , run `.trace` for more info.'
>
```
All pretty straightforward stuff. One thing to mention is that page actions and browser actions - like `openBrowser()`, `goto()` and others, have *implicit assertions*, meaning that you don't have to write code to check them to identify a failure, they simply fail - visibly. Later, we'll see some situations in which you need to provide an *explicit assertion* to determine if a test has passed. 

Type `.exit` to leave the Taiko recorder.