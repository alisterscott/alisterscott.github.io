---
title:  Code Coverage
---

## 100% Code Coverage?

Which codebase is better?

Our first codebase has **100% unit test coverage** (all paths of the code are executed at least once during test execution):

```
// divide/index.js
export default (a, b) =&gt; {
  return a / b;
};
```

```
import divide from '.';
import expect from 'expect';

describe('myAwesomeCalculator', () => {
  it('can divide two numbers', () => {
    expect(divide(35, 7)).toBe(5);
  });
});
```

Our second code base has **only 50% unit test coverage** (only half the paths through the codebase are executed during test execution)

```
export default (a, b) => {
  if (b === 0) {
    throw new Error('Cannot divide by 0');
  }
  return a / b;
};
```

```
import divide from '.';
import expect from 'expect';
import assert from 'assert';

describe('myAwesomeCalculator', () => {
  it('cannot divide by zero', () => {
    try {
      divide(5, 0);
      assert.fail('exception was not thrown');
    } catch (error) {
      expect(error).to(new Error('Cannot divide by 0'));
    }
  });
});
```

Some managers who would choose the first codebase because it has 100% unit test coverage which is much better than the code that is only 50% tested!

But code coverage is often a **watermelon:** green on the outside, red on the inside!

**Higher code coverage doesn't imply higher quality code**, because it doesn't mean higher quality tests. The accuracy and coverage of the test oracles you use determine the quality of the tests.

Beware of people boasting of high test coverage! They may only be looking at the outside of the watermelon.
