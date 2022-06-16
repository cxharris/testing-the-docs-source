---
id: Prerequisites
sidebar_position: 2
---


It turns out that many of the test tools we'll be  using have a set of common dependencies. So let's install the obvious suspects just the once. I am using Windows - if you are using MacOS or Linux, you're going to be aware of the nuances of working in your own environment and the slight differences that apply when, say, using the command line. 

If possible, install the software packages in the order in which they appear in this section - it makes some parts of this setup process a little easier.

If you are unfamiliar with these software packages, and a bit nervous about noodling around with your computer, you may find these early steps frustrating. The truth is, all computers are different and no set of installation instructions can be guaranteed to work in all cases. So please don't get despondent if it takes a little time to get this right - know that thousands of people before you have probably encountered the same issues and that help is often just a couple of internet searches away.

If you have already installed one or more of these packages, just skip the relevant section.
## Git

Wikipedia describes Git as *Software for tracking changes in any set of files*. It's a good idea to install it now, as it will be ready for us later on when we need it. As a bonus on Windows, during the installation process, you are offered (and should accept) the option of running Git inside of *Git Bash* - a Linux-like command window that's often more straightforward that the native Windows command line (and a lot lighter than PowerShell).

Get Git from https://git-scm.com/downloads, invoke the installation utility and follow the prompts through, remembering to select the options that relate to using Git via Git Bash if you are using Windows.

Even if you have never used Git before, you are likely to have heard of it and GitHub. We'll cover just a few essential Git commands here, as there is a vast amount of information already available on the web.

Importantly though, Git comes with that *Git Bash* option I mentioned earlier - and many of you may wish to hook this up into your VSCode environment (also installed later!) as a command line. 

## Node.js
When JavaScript was originated, it could only run inside a browser. Node.js is a JavaScript runtime that liberates JavaScript from the browser, allowing it to run outside of a browser, and, for example, access filesystem objects just like any other language. We will use several Node.js packages as we build up our example test suites.

You can download and install it from https://nodejs.org/en/download/ by choosing your operating system and architecture. Follow the installation instructions and the best advice is to use Google if you hit problems or need more explicit help. 

When Node.js (often called simply *Node*) has been successfully installed, you'll have access to the `node` executable in a command line or terminal.

After installing Node, you can type `node --version` in a _new_ command line or terminal - if it's been installed correctly, you'll get a reply like `v14.16.1`. Of course the precise version doesn't matter as long as you install from an obviously current download. When you install Node, you also install `npm` which stands for *Node Package Manager* - Node's default package manager, which gives you the ability to install Node's massive ecosystem of add-ons. You will need to close down and reopen any command windows or terminals before you can issue commands like `node --version` - the installation modifies your path and your environment variables get refreshed when you open a new terminal.

Once you've installed Node, we can use npm to install every other package we need - and we can do this from within VSCode's integrated terminal!

Also installed is a program called `npx` (Node Package Execute) which allows us to run any Node package that exists in the global external npm registry without even installing it. It's great for one-off initialisation of projects when we don't want the overhead of permanently installing little-used libraries.
## Visual Studio Code
Visual Studio Code (VSCode for short) is a powerful and popular source code editor available for all major platforms. Originally developed by Microsoft, most of its source code has now been released as open source under the MIT license. It's fast and extensible - you can add new functionality to it by downloading *extensions* that offer support for various programming and content creation languages - such as JavaScript and Markdown and many more.

If you already use it, that's great. If not, do yourself a favour and check it out! Which is not to say that you can't use another editor to work your way through the examples if you really want to. But it *is* the editor that I'll be using to write them, so it might be worth switching (even temporarily) just for consistency.

Visit https://code.visualstudio.com/download to get hold of Visual Studio Code. 

:::info

At some stage, the installer offers you the following options, all of which you should select (... unless you have very good and specific reasons for not doing so):
- Add "Open with Code" action to Windows Explorer file context menu
- Add "Open with Code" action to Windows Explorer directory context menu
- Register Code as an editor for supported file types
- Add to PATH (available after restart)

I've configured my Windows installation to use Git Bash as the default integrated terminal - if you'd like to do the same, you can follow the instructions here: https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal.

The other most popular options are either PowerShell or CMD, the time-honoured Windows command line - just choose the option with which you are most familiar. I hardly ever use PowerShell, so am not the right person to answer any of your PowerShell questions!

:::

### Launching VSCode and setting up a project
1. Using your preferred method, create a directory in which to manage your suite of content tests - I'm going to use `D:\content-testing-resources`. My `C` drive keeps filling up behind my back so I tend to use `D` whenever I know I have a choice!
1. Launch VSCode - you'll see a window that looks substantially like:
   
   <img src="/img/02-new-vscode-window.png" alt="Initial VSCode window" width="600"/>
1. Choose *File > Open Folder* and navigate to and select the folder you created in the first step above. You can click *Yes, I trust the authors* to give VSCode full access. This is how VSCode looks when you've done this:
   
   <img src="/img/02-vscode-in-new-folder.png" alt="Opening a directory in VSCode" width="600"/>

   If it doesn't look like this, choose *View > Explorer* from the main menu.

1. Open up a command window by typing `CTRL` + `'` - that is, `CTRL` (or the equivalent key for your own Operating System) and then `'` (apostrophe). 

   <img src="/img/02-new-command-terminal.png" alt="Opening a command terminal in VSCode" width="600"/>

   A command terminal has opened up at the bottom, below the *Welcome* pane - you can see that mine is based on bash. This little key sequence - `CTRL '` - is going to become part of your muscle memory, because we'll be using the command terminal a lot!

1. In the just-opened command terminal, type:

   ```
   npm init --yes
   ```

   This creates some small scaffolding for a Node project, ending up by generating a file called `package.json` that will ultimately contain a list of all the dependencies your project needs to run. The `--yes` parameter means that it does it all automatically, rather than bothering you with some tiresome questions about the project, which, for where we're at on our Node and Taiko journey, is just fine!

1. Click on the *Extensions* icon in the leftmost menu: <img src="/img/02-extensions-icon.png" alt="The VSCode extensions icon" width="32"/>

   Your project explorer pane is swapped for the *Extensions Marketplace* pane. In the field where it says *Search Extensions in the Marketplace*, type `project manager` - this filters out all the unrelated extensions and displays a list of project manager type extensions for VSCode. The one we want usually appears at the top of the list and is called simply *Project Manager* - you can confirm it's the right one by verifying that the author is *Alessandro Fragnani*. Click `Install` to install the extension into your VSCode setup.

   This is the general procedure for installing *any* available extension. Note that you may have to restart VSCode for the installation of *some* extensions to take effect.

1. Type `CTRL` + `SHIFT` + `P` - that is `CTRL`, then `SHIFT` (without releasing `CTRL`) and then `P` (without releasing `CTRL` and `SHIFT`) and you'll see a menu popping up offering you a list of facilities relating to your installed extension(s) - which if this is a new installation, will only involve project manager.

   Search for and select the command `Project Manager: Save Project`, then give it a name (say `content-testing-project`) and press `ENTER`. This saves your project in the project manager, so you can quickly return to it at any time in the future by relaunching VSCode and clicking the project manager icon in the left menu: <img src="/img/02-project-manager-icon.png" alt="The VSCode project manager icon" width="32"/>, which shows a selectable list of already-saved projects.

