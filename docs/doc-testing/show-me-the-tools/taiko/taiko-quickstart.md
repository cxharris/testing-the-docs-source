---
id: taiko-quickstart
sidebar_position: 1
---

# Taiko quickstart
This section is a gentle introduction to Taiko and some of the tools we've chosen to use with it. As well as presenting basic Taiko commands, it demonstrates the kind of workflows we'll use when we ramp up the complexity as we develop our test suites. 



## Quick start

After installing all of the prerequisites, you can launch Taiko by simply typing the following at the VSCode command prompt (accessible via `CTRL '` from within VSCode) at the root of your designated test folder:

```
npx taiko
```

This command downloads everything we need (if you don't already have it cached), including Chromium - the browser environment used to automate our tests. Depending on your internet connection, all this might take a couple of minutes - that Chromium download is almost 200MB.

<details>
  <summary><code>npx</code>?</summary>
  <div>
    <div> The command <code>npx</code> lets us run any Node package hosted at the central registry without installing it. Of course, there being no such thing as magic, when we use <code>npx</code> we usually have to wait for the package to download to our local system before it can run. Note that <code>npx</code> also checks to see if your package - in this case <code>taiko</code> - is the name of an executable on your system PATH or in your local project's binaries and will execute it if you have so happened to have already installed it, which you can you if you eventually get tired of waiting for it to download every time.</div>
    <br/>
  </div>
</details>



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

There are several other similarly simple commands. Try:

```
goto("https://cxharris.github.io/docs/doc-testing/intro")
```
Your browser instance flips to visit `https://cxharris.github.io/docs/doc-testing/intro`, which of course is the introduction page to this very assemblage of online content.


Now type the command:

```
click("Prerequisites")
```

You might *just* notice a red rectangle surrounding the "Prereqyuisites" item in the table of contents before it is automatically clicked and we get to the *prerequisites* page that happens to have the url https://cxharris.github.io/docs/Prerequisites.

See how the Taiko recorder keeps us up to date with the status of our work:

```
> openBrowser()
[PASS] Browser opened
> goto("https://cxharris.github.io/docs/doc-testing/intro")
[PASS] Navigated to URL https://cxharris.github.io/docs/doc-testing/intro
> click("Prerequisites")
[PASS] Clicked element matching text "Prerequisites"  1 times
```
We just issued the command `click("Prerequisites")` to tell Taiko to automatically click the table of contents link containing the text "Prerequisites". This is what's meant by Taiko's *black box* philosophy. There was no need for us to examine the underlying code of the web page - all we had to do was *look* for an onscreen object with some designated text, and ask Taiko to click it. 

### Behind the scenes
We've just run a few of Taiko's commands in its recorder.

Behind the scenes, Taiko is maintaining a list of commands for the session, and formatting them into a little JavaScript program that Taiko can run in batch mode - effectively giving you the power of repeating a sequence of commands many many times, whenever you want, without typing them in again.

To see Taiko's working copy of this code, you can just type the following from within Taiko's recorder:

```
.code
```
Don't forget the dot `.` at the beginning.

On my system, Taiko prints out:

```JavaScript
const { openBrowser, goto, click, closeBrowser } = require('taiko');
(async () => {
    try {
        await openBrowser();
        await goto("https://cxharris.github.io/docs/doc-testing/intro");
        await click("Prerequisites");
    } catch (error) {
        console.error(error);
    } finally {
        await closeBrowser();
    }
})();
```
Even if you don't call yourself a programmer, you can see the commands you've just issued - `openBrowser()`, `goto("https://cxharris.github.io/docs/doc-testing/intro")` and `click("Prerequisites")`. They happen to be surrounded by bits of JavaScript that may look strange, but you can see the general shape of the program that's getting built in the background. And what's with this `await` that precedes our commands? And what's all that other stuff like `try`, `catch` and `finally`? More of all this later, but for now, just understand that every command we type in the recorder is marshalled into this program that's accumulating in the background, and that the main *meat* of the program - its main sequence of actions - lies in that piece of the program contained in that *try block*:
```
try {
        await openBrowser();
        await goto("https://cxharris.github.io/docs/doc-testing/intro");
        await click("Prerequisites");
    }
```


#### Running a program outside the recorder
You can easily save a snapshot of the generated code to a file. To save it to a file called *getStartedTaiko.js* type:

```
.code getStartedTaiko.js
```

This immediately creates the specified file in the very directory at which you invoked Taiko in the first place.

Type `.exit` to leave the Taiko recorder and return to the VSCode command line. When you do this, the Chromium browser closes automatically.

Observe that a file called *getStartedTaiko.js* now exists in the filesystem (via `ls` or `dir` or an equivalent command). The `.js` extension is standard for JavaScript files.

We know what's inside that file, because we reviewed its contents earlier when we issued the first `.code` command. But if you wanted to browse it again, just click on the file name in the VSCode Explorer, whereupon it will open in VSCode's text editor.

From the VSCode command line, execute *getStartedTaiko.js* by typing:

```
npx taiko getStartedTaiko.js
```

On my machine, I get the following output:

```
$ npx taiko getStartedTaiko.js 
[PASS] Browser opened
[PASS] Navigated to URL https://cxharris.github.io/docs/doc-testing/intro
[PASS] Clicked element matching text "Prerequisites"  1 times
[PASS] Browser closed
```
What happened here was that we reran the tests we manually created earlier. By default, running tests this way happens in *headless* mode, where the browser operates in the background and doesn't open. But we can see that all tests passed because the key commands are tagged `[PASS]`.

If you'd prefer to see the browser going about its business, type the following instead:

```
npx taiko getSTartedTaiko.js --observe
```

### Installing Taiko properly
The downside of using the `npx` command to invoke Taiko is that it can involve a lot of waiting around for stuff to download. For me, this gets stale really quickly.

To avoid this, you can install Taiko properly - visit https://docs.taiko.dev/installing/ to review the latest installation instructions, which are quite straightforward. *Global* installation installs Taiko for use across your entire machine, while *Local* installation installs it just in the current project, which can be useful if you need to experiment with different versions of Taiko in different projects. Do not install Taiko as a `root` user. While developing this content, I opted to keep things simple and install Taiko globally. 

When you've installed Taiko this way, you can still invoke it using `npx taiko` but your installed version will be resolved, recognised and executed and you won't have to wait for the download. If you installed Taiko globally, you can also dispense with the `npx` and just issue the command `taiko` where necessary. For consistency, I will continue to use the slightly longer `npx taiko` flavour of the command.





