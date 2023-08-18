---
title: Automatically Capturing Browser Client Side Performance Logs with Playwright
---

As a lot of web apps are JavaScript heavy it's important to measure browser page performance.

Fortunately you can easily access these logs using the browser's `performance` api using Playwright.

Grabbing these performance entries as an object is as easy as calling:

```
const navTimings = await page.evaluate(() =>
  performance.getEntriesByType('navigation')
)
```

Once you have these values I've found it useful to log these out to a CSV file which can be easily opened in a spreadsheet app like Excel or Google Docs after which you can filter/sort etc.

For logging to CSV I've found it easy to use a logging library called Winston, where you write a simple custom formatter:

```
import { createLogger, format, transports } from 'winston'

const csv = format.printf(({ message, timestamp }) => {
  return `"${timestamp}",${message}`
})

export const logging = createLogger({
  format: format.combine(
    format.timestamp(),
    csv
  ),
  transports: [
    new transports.File({ filename: 'logs/pagetimes.csv' })
  ]
})
```

this allows you to easily call `logging.info('blah')` where `'blah'` is your CSV content (the logger we've created above adds a timestamp to each row automatically).

This means we can do something like this:

```
function escDoubleQuoteChars (phrase: string) {
  return phrase.replace('"', '""')
}

async function logPageLoadTimes (page: Page) {
  const navTimings = await page.evaluate(() =>
    performance.getEntriesByType('navigation')
  )
  for (const nt of navTimings) {
    let CSVStr = ''
    for (const key in nt) {
      CSVStr += `"${escDoubleQuoteChars(nt[key].toString())}",`
    }
    logging.info(CSVStr)
  }
}
```

If we want to log the header values for a header CSV row we can do this one time:

```
CSVStr += `"${escDoubleQuoteChars(key.toString())}",`
```

after which our CSV output file should contain something like:

```
"timestamp","name","entryType","startTime","duration","initiatorType","nextHopProtocol","renderBlockingStatus","workerStart","redirectStart","redirectEnd","fetchStart","domainLookupStart","domainLookupEnd","connectStart","secureConnectionStart","connectEnd","requestStart","responseStart","firstInterimResponseStart","responseEnd","transferSize","encodedBodySize","decodedBodySize","responseStatus","serverTiming","unloadEventStart","unloadEventEnd","domInteractive","domContentLoadedEventStart","domContentLoadedEventEnd","domComplete","loadEventStart","loadEventEnd","type","redirectCount","activationStart","criticalCHRestart",
"2023-08-18T03:40:25.875Z","https://webdriverjsdemo.github.io/","navigation","0","748.5999999940395","navigation","h2","non-blocking","0","0","0","0.09999999403953552","2.5","5.5999999940395355","5.5999999940395355","46.5","108.70000000298023","108.79999999701977","422.3999999910593","0","423.59999999403954","734","434","970","200","","0","0","748.0999999940395","748.0999999940395","748.0999999940395","748.3999999910593","748.3999999910593","748.5999999940395","navigate","0","0","0",
"2023-08-18T03:40:26.785Z","https://webdriverjsdemo.github.io/leave/","navigation","0","1694.8999999910593","navigation","h2","non-blocking","0","0","462.09999999403954","462.09999999403954","462.09999999403954","462.09999999403954","462.09999999403954","462.09999999403954","462.09999999403954","465.8999999910593","1346.5999999940395","0","1347","592","292","416","200","","0","0","1694.0999999940395","1694.0999999940395","1694.0999999940395","1694.8999999910593","1694.8999999910593","1694.8999999910593","navigate","1","0","0",
"2023-08-18T03:40:27.140Z","https://webdriverjsdemo.github.io/error/","navigation","0","1064.7000000029802","navigation","h2","non-blocking","0","0","427.6000000089407","427.6000000089407","427.6000000089407","427.6000000089407","427.6000000089407","427.6000000089407","427.6000000089407","428.20000000298023","750.7000000029802","0","751.2000000029802","556","256","349","200","","0","0","1064.2000000029802","1064.2000000029802","1064.2000000029802","1064.7000000029802","1064.7000000029802","1064.7000000029802","navigate","1","0","0",
"2023-08-18T03:40:28.995Z","https://webdriverjsdemo.github.io/dynamic/","navigation","0","1063.5","navigation","h2","non-blocking","0","0.10000000894069672","406.70000000298023","406.70000000298023","406.70000000298023","406.70000000298023","406.70000000298023","406.70000000298023","406.70000000298023","407.20000000298023","711.7999999970198","0","712.2999999970198","630","330","533","200","","0","0","1062.5","1062.5","1062.5","1063.2000000029802","1063.2000000029802","1063.5","navigate","1","0","0",
"2023-08-18T03:40:29.254Z","https://webdriverjsdemo.github.io/auth/","navigation","0","874.9000000059605","navigation","h2","non-blocking","0","0","176.20000000298023","176.20000000298023","176.20000000298023","176.20000000298023","176.20000000298023","176.20000000298023","176.20000000298023","176.79999999701977","492.70000000298023","0","493.90000000596046","674","374","630","200","","0","0","867.7999999970198","867.7999999970198","867.7999999970198","873.7999999970198","873.7999999970198","874.9000000059605","navigate","1","0","0",
```

We can easily open this up in Excel or even VSCode's preview mode to sort by page load times or filter by values:

![](/media/VScodeCSV.png)

If you want to see the full working code I've added to my sample repository for using Playwright in TypeScript [here](https://github.com/alisterscott/playwright-test-ts-demo).
