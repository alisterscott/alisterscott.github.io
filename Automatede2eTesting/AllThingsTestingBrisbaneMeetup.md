# All Things Testing Brisbane Presentation

# 🎭 Playwright for Automated API and Web Testing 🎭

## Welcome

Presentation online

![qr code](/media/qrcode_presentation.png)

## A bit about me:

- Test Engineer at Translink
- Artist [@juicedpixelsart](https://www.instagram.com/juicedpixelsart/)
- Volunteer at eWaste Connection

![juiced pixels](/media/juicedpixels.png)

## A bit about you:

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

