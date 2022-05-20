---
id: routine-taiko-tests
sidebar_position: 2
---

# Routine Taiko tests
This section implements our set of standard tests using Taiko.

## Bring on the tests

### Check that a content page is alive
From the Taiko recorder, we visit `https://cxharris.github.io/docs/intro` and accept their cookie warning if it is present. 

In the Taiko recorder, type:

```
> openBrowser()
> goto("https://cxharris.github.io/docs/intro")
>
```
Taiko will command the open browser to visit the specified page.

Success looks like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs/intro")
[PASS] Navigated to URL https://cxharris.github.io/docs/intro
>
```
A failed visit would look like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs/intro")
'[FAIL] Error: Navigation to url https://cxharris.github.io/docs/intro failed.
' +
  ' STATUS: 404, STATUS_TEXT: , run `.trace` for more info.'
>
```
All pretty straightforward stuff. One thing to mention is that page actions and browser actions have *implicit assertions*, meaning that you don't have to check them to identify a failure, they simply fail. Later, we'll see some situations in which you need to provide and *explicit assertion* to determine if a test has passed.