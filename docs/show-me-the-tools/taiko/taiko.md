### Installing Taiko using npm
In the command window type:
```
npm install taiko
```

Be sure to be in a command window at the root of your project when you do this - your output will probably look a lot like mine, and you can ignore any `WARN` messages at this stage:

```
clive@DESKTOP-AV6MK69 MINGW64 /d/content-testing-book
$ npm install taiko
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated

> taiko@1.2.7 install D:\content-testing-book\node_modules\taiko
> node lib/install.js

Downloading Chromium r823078 - 154.7 Mb [====================] 100% 0.0s

> taiko@1.2.7 postinstall D:\content-testing-book\node_modules\taiko
> node lib/documentation.js

npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.3.2 (node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
npm WARN content-testing-book@1.0.0 No description
npm WARN content-testing-book@1.0.0 No repository field.

+ taiko@1.2.7
```

This command goes off, locates Taiko, and installs it as a Node package in your local project directory - it (i.e. Taiko) will only be available for this project, from a command line that's open inside a project directory, rather than globally. I'll be brutally honest here, the only reason we are choosing to do it *locally* is that there's currently a bug affecting global installs! There's a workaround, but a local install is much less hassle.

Also downloaded is a version of Chromium - an open source codebase (and its binaries) for a web browser that forms the baseline for several industry-leading browsers, like Chrome and Edge (... but not, as it turns out, Firefox). Our tests are going to take shape when we automate this special installation of Chromium to visit web pages. Lots of information messages and a few warnings (which can be safely ignored) appear during this process.

To be fair, this can take some time, depending on your internet speed. When it's finished, you'll see in your project explorer that a directory called `node_modules` has been created. If you're of a curious disposition, you can review `package.json` and see that it's had a new dependency added by the installation process:

```Json
...
  "dependencies": {
    "taiko": "^1.2.7"
  },
...
```
You might also notice that `node_modules` contains a shedful of files and directories! Again, no worries - that's how Node works.

To check it's worked, make sure your command line is open at the root of your project (in my case this is `D:\content-testing-book` or `d/content-testing-book` in bash) and type:

```Bash
$ ./node_modules/.bin/taiko

Version: 1.2.7 (Chromium: 88.0.4314.0)
Type .api for help and .exit to quit

>
```
Notice how the command prompt has changed from the bash command prompt to Taiko's: `>`.

Well done, we've come a long way and are nearly ready for some fun. If you've had trouble installing Taiko, check out the docs site: `https://docs.taiko.dev/`.

One final but important word - to get out of Taiko and back to the command terminal proper, you need to type `.exit` (don't forget the dot) at the Taiko prompt.

In the next section, we'll learn a lot about Taiko and start to put it through its paces. All this setup can be a bit of a drag, especially if you hit problems along the way. It always makes me feel better when I realise that it's a one-off activity - you'll probably never have to do all of it again.

