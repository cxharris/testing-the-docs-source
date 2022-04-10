---
sidebar_position: 1
---

# Why automate doc testing?

Being able to deliver your docs online instead of in printed form is a welcome blessing for most tech writers. But there **can** be a few headaches.  If you can publish thousands of pages at the press of a button, repeatedly, it becomes impossible to manually check final outputs for correctness each and every time. Errors creep in - and when they do, it can get messy very quickly. What's needed is a way to use the power of automation to test and validate our content - at least at every publishing event, eliminating a lot of the tedium and mistakes that happen when human beings are forced to do the job. Even better, if this task can be performed by the very same technical writers and content developers who maintain the information in the first place, then we can set up a virtuous feedback loop that amplifies the power of our teams.

Ever since there have been online web applications, engineers have sought to use computers to test them. *Automated browser testing tools*, as they are called, are a well-established segment of the software industry, but there's a huge latent potential for their productive use in documentation and technical content workflows as well as their well-established presence in the software development lifecycle. What's more, in the case of online content, the universe of possible tests is vastly smaller than is the case with broader software development, which bodes well for how quick it is going to be to get up to speed with these new concepts and techniques in a documentation and content context. 
## Use cases

In case you're wondering what kinds of things it's possible to automatically test, here's a taster:

- Checking that your content delivery site is up and available in the first place
- Validating that a new topic or article has made it through to the latest published version
- Ensuring that all headers/footers reference the correct version for the publication
- Checking that a page contains (or does not contain) some specific required (or proscribed) item of content or text
- Confirming that a documentation defect has been fixed and tracked into production
- Checking that the table of contents is complete and points to live, available topics
- Ensuring that there are no instances of common mis-spellings of words, especially jargon words or words specific to your organisation
- Making sure that all content site links are valid
- Confirming that all pages have the correct security/confidentiality markings where relevant
- Affirming that legal boilerplate text is correct and up-to-date
- Identifying situations where there are inconsistencies across the site
- Being part of the effort to prevent proscribed information from leaving a secure facility, such as a data room

What can make things challenging is that there's no one-size-fits-all approach to these tests. It depends on all sorts of factors relating to how your content website was built or generated. In addition, in the EU at least, there are often cookie-warning popups that have to be navigated before the actual contents of a site can be examined. All of this combines to make the effort non-trivial but worth it in the end - you'll be in a position where you can hear the alarm bells ringing well before senior management is even aware that anything is wrong!

### A programming mindset
One dimension in which automated testing tools vary is in the amount of programming knowledge required by their users. There are indeed online testing systems that require no programming knowledge at all. Equally, there are those that are specifically targeted at software development professionals and require deep understanding of a language and its idioms. Life being what it is, the tools at the 'no programming' end of the spectrum are very often not powerful or fluent enough to do the jobs technical writers and other content developers need them to do. We need to find a *sweet spot* in complexity - a place where we have the power and expressiveness we need, but not to overdo it and have to pay a consequent cost in terms of cognitive overhead and reduction in productivity.

As it happens, several tools successfully walk this line between complexity and ease of use and we will meet a selection as we progress through the chapters. We'll also be working with the open source Visual Studio Code editor (known more commonly as simply *VSCode* and not to be confused with the closed source Microsoft product *Visual Studio*. Sheesh.) and a number of recommended extensions - but more about VSCode later.

Most of the time we will be issuing commands to a tool that records our desired test actions and *generates* and saves the code of a program in JavaScript. So most of the time, to the extent that we will need to program at all, we will need to make changes to that generated code, often small changes, rather than create standalone programs. Why JavaScript? Well, it jives well with the ecology of browsers and the web and the most suitable automated test tools for our purposes all use JavaScript as their base language. 

As a first glimpse of what I mean, here is the full (generated) program code of a test that visits `https://www.wikipedia.org/` to simply check that it is alive and kicking:

```JavaScript
const { openBrowser, goto, closeBrowser } = require('taiko');
(async () => {
    try {
        await openBrowser();
        await goto("https://www.wikipedia.org/");
    } catch (error) {
        console.error(error);
    } finally {
        await closeBrowser();
    }
})();
```
Even if you've never written a line of JavaScript in your life, and even if you think the above code looks rather complicated, it's pretty obvious that most of the interesting action happens in the line 

```JavaScript
await goto("https://www.wikipedia.org/");
```
You're probably already thinking that there's a fair chance that if you change the Wikipedia URL to a different valid URL, you'll change the test to check that different site instead - and you'd be right! You don't have to understand much more than this to make a good start in building your own library of content tests.

But enough, we're already ahead of ourselves!
## Goals
If it isn't obvious, what we're shooting for here is a way to improve the quality, reliability and timeliness of a typical online publishing lifecycle, without busting the budget or requiring large injections of unfunded resources. Incidentally, and to reiterate what is stated in the preamble, none of the techniques described will be limited to *software documentation* - they apply equally to other types of published output involving media, words and images - online magazines, newspapers and so on. If something reaches a user via a browser and html, then it is fair game for us!

## Audience
This book is written for content developers for whom it might be a very first journey into test automation as applied to creating and testing the online word. If you have a software development background, or years in programming-related roles, it is very possible that you will find alternative and perhaps more suitable solutions for your own specific needs. 

## What to expect from here on in

Following this introduction, we cover the following areas - it's recommended that you work through them in the order presented:

- Setting things up - installing required software
- A first proof-of-concept test
- Checking pages for the right content
- Organising testing, playback and reporting
- Opening the hood on Taiko and JavaScript
- Adding new functionality
- Dockerising your content testing environment

Let's discover **Docusaurus in less than 5 minutes**.

## Getting Started

Get started by **creating a new site**.

Or **try Docusaurus immediately** with **[docusaurus.new](https://docusaurus.new)**.

### What you'll need

- [Node.js](https://nodejs.org/en/download/) version 14 or above:
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.

## Generate a new site

Generate a new Docusaurus site using the **classic template**.

The classic template will automatically be added to your project after you run the command:

```bash
npm init docusaurus@latest my-website classic
```

You can type this command into Command Prompt, Powershell, Terminal, or any other integrated terminal of your code editor.

The command also installs all necessary dependencies you need to run Docusaurus.

## Start your site

Run the development server:

```bash
cd my-website
npm run start
```

The `cd` command changes the directory you're working with. In order to work with your newly created Docusaurus site, you'll need to navigate the terminal there.

The `npm run start` command builds your website locally and serves it through a development server, ready for you to view at http://localhost:3000/.

Open `docs/intro.md` (this page) and edit some lines: the site **reloads automatically** and displays your changes.
