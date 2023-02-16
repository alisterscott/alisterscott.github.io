The page object pattern is a classic pattern to model application state (pages) and things you do (or an automated test tool does) to them.

There's often [negativity](https://www.fastcompany.com/3052222/hit-the-ground-running/the-problem-with-best-practices) towards _best practices_, but I can confidently say that **page objects _are_ a best practice** for test automation of UI systems, which isn't saying they will be exactly the same in every context, but there's a common best practice pattern there which you can use.

Page objects, as a pattern, typically:

1.  Inherit from a base page object/container which stores common actions like:
    - instantiating the object looking for a known element that defines that page's existence
    - optionally allow a 'visit' to the page during instantiation using some defined URL/path
    - provides actions and properties common to all pages, for example: waiting for the page, checking the page is displayed, getting the title/url of the page, and checking cookies and local storage items for that page;
2.  Define actions as methods which are ways of interacting with that page (such as logging in);
3.  Do not expose internals about the page outside the page -- for example they typically don't expose elements or element selectors which should only be used within actions/methods for that page which are exposed; and
4.  Can also be modeled as _components_ for user interfaces that are built using components to give greater re-usability of the same components across different pages.

The biggest benefit I have found from using page objects as a pattern is having more deterministic end-to-end tests since instantiating a page means you know you are on that page, so the automated tests will fail more reliably with a better understanding of what went wrong.
