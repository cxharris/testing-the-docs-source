---
sidebar_position: 1
---

# Tools and tests

## Tests
Here are the initial simple tests we plan to automate in each of a selection of test tools:

1. Check that a content page is alive - that your doc site is up and running.
2. Confirm that a content page has a specific heading.
3. Confirm that a content page does not contain some out-of-date text.
4. Validate that a table-of-contents link ends up on the right page.

We'll later add more tests, doing a deeper dive into some more complex situations.

## Tools

### Taiko

Taiko (https://taiko.dev/) is an open-source node.js library for testing web applications. We will meet several such tools but Taiko is the right one to start with - it's accessible and offers several powerful test capabilities before you have to resort to programming (which, let it be said, is definitely required for anything like a production-quality test suite).

Taiko's web site claims it:

* Treats a browser like a black box, so that we can write tests just by *looking* at a web page, not inspecting its underlying source code.
* Implicitly waits for network-related events to finish, reducing the number of failed tests.
* Includes a recorder with which you can record and write tests, later expanding them to full programs if you wish.

All of which is true - until it's not!

### Test Cafe

### Cypress

### Playwright



