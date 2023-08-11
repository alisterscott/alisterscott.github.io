---
title: Parallel Execution
---

One of the best ways to speed up your end-to-end (e2e) tests is to start running them in parallel.

The main issue I see that prevents teams from fully using parallelism for their e2e tests is lack of test design. Without adequately designed e2e tests -- which have been designed to be run in parallel -- parallelism can introduce non-deterministic and inconsistent test results -- leading to frustration and low-confidence in the e2e tests.

This is often the case when teams go about directly converting manual test cases into automated e2e tests -- instead of approaching e2e test automation with a specific end-to-end design focus.

Say you had a manual test case for inviting someone to view your WordPress blog:

1.  Enter the email address of the person you'd like to follow your site
2.  Check the list shows a pending invite
3.  Check your email inbox shows a pending invite
4.  Open the email, follow the link and sign up for a new account

When you're manually testing this in sequence it's easy to follow -- but as soon as you start running this in parallel, across different builds, and with other tests things will most likely start failing.

Why? The test isn't specific enough -- you may have multiple pending invites -- so how do you know which one is which? You can only invite someone once, how do you generate new invite emails? You may receive multiple emails at any one time -- which one is which? And more.

With appropriate e2e test design you can write the e2e test to be consistent when run regardless of parallelism:

1.  Email addresses are uniquely generated for each test run using a [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) and either a test email API like Mailosaur or Gmail plus addressing; and
2.  The pending email list has a data attribute on each invite clearly identifying which email the invite is for and this is used to verify pending email status; and
3.  The inbox is filtered by the expected GUID, and only those emails are used. Etc.

Once you have good e2e test design in place you're able to look at how to speed up e2e test execution using parallelism. I'll cover how to do this in my next blog post.
