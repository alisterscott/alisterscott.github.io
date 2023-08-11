---
title: Automatically checking for browser console errors using Playwright
---

I like using automated end to end tests to check for browser console errors whenever they're running as I've found this useful in discovering unexpected bugs across web apps I have worked on.

Fortunately this is rather easy to do in Playwright with some simple page fixture code which then applies to every test without having to do any additional instruction.

We create a file like `fixtures.ts`:

```
import { test as base, expect } from '@playwright/test'

export const test = base.extend({
  page: async ({ page }, use) => {
    const messages: string[] = []
    page.on('console', (msg) => {
      if (msg.type() === 'error') {
        messages.push(`[${msg.type()}] ${msg.text()}`)
      }
    })
    page.on('pageerror', (error) => {
      messages.push(`[${error.name}] ${error.message}`)
    })
    await use(page)
    expect(messages).toStrictEqual([])
  }
})

export default test
```

and all we have to do in our tests is import the test object from our fixture file instead of using the default Playwight one.

For example:

```
import { test } from '../fixtures'
import { expect } from '@playwright/test'
import { visitHomePage } from '../lib/actions/nav'

test.describe.parallel('All tests', () => {
  test('can automatically check for errors on every page', async ({ page }) => {
    test.fail()
    await goToPath(page, 'error')
  })
})
```

each time we use the `{ page }` fixture in a test it automatically checks for console errors and fails the test if any appear.
