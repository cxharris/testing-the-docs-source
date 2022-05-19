---
id: routine-taiko-tests
sidebar_position: 2
---

# Routine Taiko tests
This section implements our set of standard tests using Taiko.

## Bring on the tests

### Check that a content page is alive
From the Taiko recorder, we visit `https://stripe.com/docs` and accept their cookie warning if it is present. 

Type:

```
> openBrowser()
> goto("https://stripe.com/docs")
> click("Accept all")
>
```
The `click("Accept all")` command clicks a button that signifies that you, the site visitor, accepts their cookie usage. If it doesn't appear, it's likely you are in a part of the world that doesn't have to bother about such things!

Success looks like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://stripe.com/docs")
[PASS] Navigated to URL https://stripe.com/docs
> click("Accept all")
[PASS] Clicked element matching text "Accept all"  1 times
>
```
Failing the visit to the entire page looks like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://stripe.com/does-not-exist")
'[FAIL] Error: Navigation to url https://stripe.com/does-not-exist failed.
' +
  ' STATUS: 404, STATUS_TEXT: , run `.trace` for more info.'
>
```
Failing the cookie warning looks like:
```
> openBrowser()
[PASS] Browser opened
> goto("https://stripe.com/docs")
[PASS] Navigated to URL https://stripe.com/docs
> click("I am not a button")
[FAIL] Error: Element with text I am not a button not found, run `.trace` for more info.
>
```
All pretty simple, and it's evident that the Stripe documentation site responds with a 404 error when you try to visit a non-existent page.