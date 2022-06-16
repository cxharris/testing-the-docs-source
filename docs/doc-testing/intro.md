---
id: intro
sidebar_position: 1
---

# Automated doc testing

Being able to deliver our docs online instead of in printed form is an overdue but welcome blessing for most tech writers. But there _can_ be a few headaches. Our ability to repeatedly publish thousands of pages at the press of a button makes it impossible to review the outputs for correctness each time. Errors creep in - and when they do, it can get messy very quickly. 

What's needed is a way to harness the power of automation to test and validate our content, eliminating a lot of the tedium and mistakes that happen when human beings are forced to do the job. Even better, if this task can be performed by the same technical writers and content developers who maintain the information in the first place, then we can set up a virtuous feedback loop that amplifies the power of writing teams.

*Automated browser testing tools* are a well-established segment of the software industry, used by engineers everywhere to test their web applications. But there's also a huge latent potential for their productive use in online documentation and technical content workflows. What's more, with online content, the universe of possible tests is vastly smaller than is the case across the whole of software development, making the entire proposition eminently workable, even for very small teams and even solo writers.
## Use cases

In case you're wondering what kinds of things it's possible to automatically test, here's a taster:

- Checking that your content delivery site is up and available in the first place
- Validating that a new topic or article, or even just a changed sentence, has made it through to the latest published version
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

What can make things challenging is that there's no one-size-fits-all approach to such tests, and they all require resources to develop and maintain. 

It turns out that very often, these resource requirements are modest and can be easily accommodated in typical project budgets. Moreover, if output accuracy and quality is especially important to you, then their value becomes even greater.

### Batteries not included
For the sake of being explicit, we are _not_ in the business of using automated tests to drive the execution of embedded code examples. This is a great idea and is done well in the Rust documentation (https://doc.rust-lang.org/rustdoc/documentation-tests.html). In the present context, our goal is to explore an approach to testing and validating _regular content_ itself - something that seems to have been neglected in common practice.

Neither do we examine how to test PDF outputs. As an *output* format, PDF rarely contains enough information to enable the reconstruction of source-level content, making testing particularly difficult. A series of articles on testing PDF outputs - given these constraints - is planned for the future.

## If we only had a plan!
Remember I said there's no one-size-fits-all kind of solution? So we're going to explore a bunch of automated test tools that vary in their approaches, and assess them for their suitability for testing doc output, implementing the same set of tests in each of the different tools, so that you can form a valid judgment of what jives best with your writing practices and testing needs.

For a sample document, we'll use the pages you're currently reading on this very site (http://cxharris.github.io), with occasional side-quests to other sites built with different technologies.
## Audience
If you're a technical writr or content developer who has never explored the idea of automated testing, this material if for you! If you've been using automated testing for some time, then you'll probably be better served elsewhere, sorry!

If you're still with us, you _will_ need to be a little familiar with a programming mindset - JavaScript experience in particular would be a lot of help. While I won't explain the absolute basics (... plenty of online resources already do that) I'll be sure to point out when and where the code verges on the idiomatic and is potentially confusing.

But learn some JavaScript - it's fun! It will be especially useful if you work for a company outside the immediate tech sphere, such as, say, a small manaufacturing company that publishes assembly instructions on its website. 

### Learning pathways
If you are new to the whole idea of applying automated testing techniques to documentation, then work your way through the Taiko material. Even if Taiko is not on your tools shortlist and you decide not to use it - the experience will give you a great overview of how these frameworks operate, and introduce you to several vital techniques, regardless of your ultimate tool choice.

The very same Taiko material would suit someone who wanted to begin to understand how automated end-user testing works, although he or she would have to find some more rigorous material later.

If you're cool with and understand about automated testing tools, then you can pick and choose from the several tools offered.

