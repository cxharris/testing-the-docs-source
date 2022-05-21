---
id: taiko-validate-page-title
sidebar_position: 2
title: Validate page title
---

# Validate a page title

## Plan
Check out this page and observe that its title is *Test page | Testing the docs*: `https://cxharris.github.io/docs`. The *title* is the text that occupies the browser tab, and not the so-called *title* of the topic displayed on the page.

First we'll use the Taiko recorder to visit `https://cxharris.github.io/docs`, and use the `title()` command to display the page title. 

Then we'll save the generated code to a file, modifying it with some further simple commands to validate that the page title is correct. 

This extended workflow is another small but significant step in our learning, taking us closer to being able to write fully-developed tests that can validate all content. Eventually, you will be able to skip using the Recorder all together.

## Implementation
In the Taiko recorder, type:

```
> openBrowser()
> goto("https://cxharris.github.io/docs")
> title()
```
Taiko commands the browser to visit the specified page and output the title text.

```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs")
[PASS] Navigated to URL https://cxharris.github.io/docs
> title()
'Test page | Testing the docs'
```

Save the so-far-generated code by typing:

```
.code validateTitleTaiko.js
```
Type `.exit` to leave the Taiko recorder.

### Generated code

Examine the saved file `validateTitleTaiko.js`:
```
const { openBrowser, goto, title, closeBrowser } = require('taiko');
(async () => {
    try {
        await openBrowser();
        await goto("https://cxharris.github.io/docs");
        await title();
    } catch (error) {
        console.error(error);
    } finally {
        await closeBrowser();
    }
})();
```
Check that you can replay this little bit of generated test code by typing the following at the VSCode command prompt (*not* the recorder):
```
taiko validateTitleTaiko.js
```
You should get a confirmation with the output:
```
$ taiko validateTitleTaiko.js 
[PASS] Browser opened
[PASS] Navigated to URL https://cxharris.github.io/docs
[PASS] Browser closed
```
Remember that by default when we run our test code like this (as opposed to in the Recorder) the browser runs in *headless* mode, so we can't see it. Note also, in passing, how it seems that the `await title()` command didn't produce any output.

### Changing the generated code
#### Preparing the way
First, type the following at the VSCode command prompt:

```
npm install assert
```
This installs Node's `assert` module allowing us to use explicit assertions, which we'll get to in a few moments. Taiko supports several assertion libraries/modules, but here we've opted to use Node's.

#### Adding some new commands
In the VSCode editor, beneath the line `const { openBrowser, goto, title, closeBrowser } = require("taiko");` add the line:
```
const assert = require("assert").strict;
```
This tells Node to make the *strict* version of its `assert` module available, whch allows us to use Node's *assertions*. There is no real need to be concerned about what `strict` means in this context - it's present for historical reasons but makes sense to use most of the time nowadays.

Change the line `await title();` to:
```
assert.equal(await title(), "Test page | Testing the docs");
```
Here, we are making the claim (or assertion) that the title of the page should be equal to `Test page | Testing the docs`.

<details><summary>What are assertions anyway? And what is <code>await</code> for that matter?</summary>
<div>
Let's deal with <code>await</code> first. Some commands can take a long time to complete - usually a long time in computer terms, which is often still a very short time in human terms. These commands are often commands that invoke network calls whose responsiveness cannot be predicted or guaranteed. 
<br/><br/>
They take as long as they take, which can vary from day to day or hour to hour, depending on your network's situation (and the situations of all the intermediate networks between your machine and your command's ultimate target). All we're saying when we write `await title()` is "Go off and find me the title of the current web page, take as long as it takes and let me know when you've finished. I won't start anything else until you've finished - I'll <i>await</i> your completion. By the way, if you take too long, I'll simply abort."


Generally, an assertion is a statement that something is the case. Or not.


</div>
</details>

Save the file and check that it now looks like:
```
const { openBrowser, goto, title, closeBrowser } = require("taiko");
const assert = require("assert").strict;

(async () => {
  try {
    await openBrowser();
    await goto("https://cxharris.github.io/docs");
    assert.equal(await title(), "Test page | Testing the docs");
  } catch (error) {
    console.error(error);
  } finally {
    await closeBrowser();
  }
})();
```
Finally, having edited and saved it, run it:
```
taiko validateTitleTaiko.js
```
## Results

If the tests pass, you'll see the following output:
```
$ taiko validateTitleTaiko.js 
[PASS] Browser opened
[PASS] Navigated to URL https://cxharris.github.io/docs
[PASS] Browser closed
```
Note again that the `assert` statement produces no output if successful!

If the `assert` fails, you'll see:
```
$ taiko validateTitleTaiko.js 
[PASS] Browser opened
[PASS] Navigated to URL https://cxharris.github.io/docs
AssertionError [ERR_ASSERTION]: Expected values to be strictly equal:
+ actual - expected

+ 'Test page | Testing the docs'
- 'Test page | This doesnt exist'
                ^
    at D:\information-products\content-testing\code-samples\taiko\validateTitleTaiko.js:8:12 {
  generatedMessage: true,
  code: 'ERR_ASSERTION',
  actual: 'Test page | Testing the docs',
  expected: 'Test page | This doesnt exist',
  operator: 'strictEqual'
}
[PASS] Browser closed
```
At last we've managed to get the `assert` statement to speak to us! All is well and good here - when the assertion passes, no superfluous output is generated, but when it fails, we get ample information.