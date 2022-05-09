# Taiko quickstart
This section is a gentle introduction to Taiko and some of the tools we've chosen to use with it. As well as presenting basic Taiko commands, it demonstrates the kind of workflows we'll use when we ramp up the complexity as we develop our test suites. 



## Quick start

After installing all of the prerequisites, you can launch Taiko by simply typing the following at the VSCode command prompt (accessible via `CTRL '` from within VSCode) at the root of your designated test folder:

```
npx taiko
```
<details>
  <summary><b>npx</b></summary>
  <div>
    <div> ... recall that the command <b>npx</b> lets us run any Node package hosted at the central registry without installing it. Of course, there being no such thing as magic, when we use `npx` we usually have to wait for the package to download to our local system before it can run. Note that `npx` also checks to see if your package - in this case `taiko` - is the name of an executable on your system PATH or in your local project's binaries and will execute it if you have so happened to have already installed it, which you can you if you eventually get tired of waiting for it to download every time.</div>
    <br/>
  </div>
</details>

It also downloads Chromium - the browser environment used to automate our tests. Depending on your internet connection, all this might take a couple of minutes - that Chromium download is almost 200MB.

When it's done, you'll end up in the Taiko *recorder*:

```
$ npx taiko
Downloading Chromium r967620 - 177.1 Mb [====================] 100% 0.0s

Version: 1.3.2 (Chromium: 100.0.4874.0)
Type .api for help and .exit to quit

>
```
Taiko's *recorder* is a special command line interface designed to execute Taiko commands.

<details>
<summary>Command line interfaces</summary>
<div>
We'll frequently use two command line interfaces - the one within VSCode, and Taiko's *recorder*. It's important, particularly when starting out, to be aware of *which* command line interface you are using - you can usually tell which is which by examining the command line prompt.

* The VSCode command line prompt might be a `$` sign (for Git bash) or it might look like a file path followed by an angle bracket (e.g. C:\my-taiko-tests >) if you've chosen to use CMD rather than Git bash. 
* The Taiko command prompt is an isolated right angle bracket: `>` and you get to it by entering the command `npx Taiko` at the VSCode command prompt. So the VSCode command prompt is on the road to Taiko.

Don't worry too much about this - it's worth mentioning at this point, to try to avert confusion, but we'll get plenty of practice at using both.
</div>
</details>

### Automating a browser
From within Taiko's recorder, type the following and hit ENTER:

```
openBrowser()
```

You'll see an instance of the Chromium browser appear in its own new window. To be sure, if it *doesn't* appear, we're in big trouble! 

Mine looks like this:

   <img src="/img/initial-chromium-window.png" alt="Chromium's initial window" width="600"/>

We just issued the `openBrowser()` command to Taiko, and it duly opened a browser instance. Taiko also issued a `[PASS]` message in its recorder output to indicate that it was successful in executing our command:

```
> openBrowser()
[PASS] Browser opened
```
If you have more than one monitor, it's always useful to drag the Chromium browser window to some free screen real estate, so that we can see both the VSCode window where we issue commands to the recorder, and the corresponding actions it invokes on the browser instance itself. If you've just one monitor, then the best thing to do is to tile your windows as best you can.

There are other commands, try:

```
goto("google.com")
```
Your browser instance goes to `google.com` and displays Google's cookie warning dialog:

   <img src="/img/google-cookie-warning.png" alt="Google cookie warning dialog" width="600"/>

This is because when a Taiko browser session starts, it creates an environment without any cookies - to ensure that every 'test' begins in the same state. So we have to navigate our way through this. It has no memory of when you, as an individual, last used your browser to visit Google - it's as if someone visited the site for the first time. That's why we get the boring cookie warnings.

Type the command:

```
click("I agree")
```

You might *just* notice a red rectangle surrounding the "I agree" button in the browser before it is automatically clicked and we get to the regular Google home page.

See how the Taiko recorder keeps us up to date with the status of our work:

```
> openBrowser()
[PASS] Browser opened
> goto("google.com")
[PASS] Navigated to URL http://google.com
> click("I agree")
[PASS] Clicked element matching text "I agree"  1 times
>
```

:::note

It's possible that due to your location or other factors, you may not get the Google cookie warning dialog. If this is the case, the `click("I agree")` test will fail and you'll see a failure message in your Taiko output:

```
[FAIL] Error: Element with text I agree not found, run `.trace` for more info.
```

:::

Look how we just issued the command `click("I agree")` to automatically click the button with the "I agree" text. This is what's meant by Taiko's *black box* philosophy. There was no need for us to examine the underlying code of the web page - all we had to do was *look* for an onscreen object with some designated text, and ask Taiko to click it. 

### Behind the scenes
We've just run a few of Taiko's commands in its recorder.

Behind the scenes, Taiko is maintaining a list of commands for the session, and formatting them into a little JavaScript program that can run on its own - effectively giving you the power of repeating a sequence of commands many many times, whenever you want, without typing them in again.

To see Taiko's working copy of this code, you can just type the following from within Taiko's recorder:

```
.code
```
Don't forget the dot `.` at the beginning.

On my system, Taiko prints out:

```
const { openBrowser, goto, click, closeBrowser } = require('taiko');
(async () => {
    try {
        await openBrowser();
        await goto("google.com");
        await click("I agree");
    } catch (error) {
        console.error(error);
    } finally {
        await closeBrowser();
    }
})();
```
Even if you don't call yourself a programmer, you can see the commands you've just issued - `openBrowser()`, `goto("google.com")` and `click("I agree")`. They happen to be surrounded by bits of JavaScript that may look strange, but you can see the general shape of the program that's getting built in the background. And what's with this `await` that precedes our commands? And what's all that other stuff like `try`, `catch` and `finally`? More of all this later, but for now, just understand that every command we type in the recorder is marshalled into this program that's accumulating in the background, and that the main *meat* of the program - its main sequence of actions - lies in that piece of the program contained in that *try block*:
```
try {
        await openBrowser();
        await goto("google.com");
        await click("I agree");
    }
```


#### Running a program outside the recorder