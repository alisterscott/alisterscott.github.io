---
title: All Things Testing Brisbane Presentation
---

## 🎭 Playwright for Automated API and Web Testing 🎭

<nav>
  <h4>Table of Contents</h4>
  * this unordered seed list will be replaced by toc as unordered list
  {:toc}
</nav>

## Welcome

Presentation online

![qr code](/media/qrcode_presentation.png)

## A bit about me

- Test Engineer at ~~Aurion~~ Translink
- Artist [@juicedpixelsart](https://www.instagram.com/juicedpixelsart/)
- Volunteer at eWaste Connection

![juiced pixels](/media/juicedpixels.png)

## A bit about you?

1. Raise your hand if you're heard of Playwright
2. Keep it raised if you've used Playwright before
3. Keep it raised if you're currently using Playwright in your day job

## A bit about [Playwright](https://playwright.dev/)

![Test tool evolution](/media/toolevolution.png)

[Original Image Creative Commons](https://commons.wikimedia.org/w/index.php?curid=2165296)

- Open source library backed by Microsoft spawned from Puppeteer
- Supports Chrome, Edge, Firefox & Safari
- Supports Node.js, Python, Java & .NET
- Web API and Browser Automation
- Automatic waiting for everything - very rare to have to write a wait statement 😊
- Full parallel test execution support inc. locally
- Headless by default but can run 'headed' and doesn't take over your computer
- Actively growing community and features
- Official VSCode extension with full debugging capability
- I have used for over 2 years on 2 different projects with _great success_

## Playwright 101 - Playwright Test in Node 

```
import { test, expect } from '@playwright/test';

test('this presentation has a title', async ({ page }) => {
  await page.goto('https://alisterscott.github.io/Automatede2eTesting/AllThingsTestingBrisbaneMeetup');
  const title = page.locator('#all-things-testing-brisbane-presentation');
  await page.screenshot({ path: 'webpage.png' });
  await expect(title).toHaveText('All Things Testing Brisbane Presentation');
});
```

▶️ run this here: [https://try.playwright.tech/?l=playwright-test&s=cnsqj5b](https://try.playwright.tech/?l=playwright-test&s=cnsqj5b)

## Recording video and interacting with elements

### Example Form

<form>
  <label for="fname">First name:</label>
  <input type="text" id="fname" name="fname"><br><br>
  <label for="lname">Last name:</label>
  <input type="text" id="lname" name="lname"><br><br>
  <input type="submit" value="Submit">
</form>

### Test

```
import { test, chromium } from '@playwright/test';

test('can record a video of form interaction', async ({}) => {
  const browser = await chromium.launch({ slowMo: 2000 });
  const context = await browser.newContext({
    recordVideo: {
      dir: 'videos/'
    }
  });
  const page = await context.newPage();
  await page.goto('https://alisterscott.github.io/Automatede2eTesting/AllThingsTestingBrisbaneMeetup');
  await page.getByLabel('First name:').fill('Horsey');
  await page.getByLabel('Last name:').fill('Hippo');
  await page.getByRole('button', { name: 'Submit' }).click();
  await context.close();
});
```
▶️ run this here: [https://try.playwright.tech/?l=playwright-test&s=91ho6pk](https://try.playwright.tech/?l=playwright-test&s=91ho6pk)

## API Testing

Calling APIs is as easy as controlling a browser:

### API Testing (Assertion Style)

```
import { test, expect } from '@playwright/test';

test('can GET a REST API and check response using assertion style', async ({ request }) => {
  const response = await request.get('https://my-json-server.typicode.com/alisterscott/alisterscott.github.io/posts')
  expect(response.status()).toBe(200)
  const body = JSON.parse(await response.text())
  expect(body.length).toBe(3)
  expect(body[0].id).toBe(1)
  expect(body[0].title).toBe('Aardvarks')
  expect(body[1].id).toBe(2)
  expect(body[1].title).toBe('Baboons')
  expect(body[2].id).toBe(3)
  expect(body[2].title).toBe('Cats')
})
```
### API Testing (Approval Style)


You can also do 'approval' style testing where you store a snapshot of the response in your source code, and your test fails if this changes:

```
import { test, expect } from '@playwright/test';

test('can GET a REST API and check response using assertion style', async ({ request }) => {
  const response = await request.get('https://my-json-server.typicode.com/alisterscott/alisterscott.github.io/posts')
  await expect(response, `Response: ${await response.text()}`).toBeOK()
  const body = await response.text()
  expect(body).toMatchSnapshot('post.txt')
})
```

where `post.txt` is generated on first run to contain:

```
[
  {
    "id": 1,
    "title": "Aardvarks"
  },
  {
    "id": 2,
    "title": "Baboons"
  },
  {
    "id": 3,
    "title": "Cats"
  }
]
```


