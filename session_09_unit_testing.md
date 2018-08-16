


## Jest
Jest is a test runner. It provides a formula for writing unit tests but it also
has the ability to run those tests for you.

### Configure Jest
We've been using `react-scripts` in our `developer-toolcamp-ui` project which
bundles Jest as part of it.

We're already using `react-scripts` to start our application so all we need to
do is update our `package.json` file to call `react-scripts` for testing as
well.

**package.json**
```
"scripts": {
  "start": "react-scripts start",
  "test": "react-scripts test"
},
```

### Add a unit test
Let's add a simple function to our application to test, in a new file called
`add.js` within the `src/` folder:  

**add.js**
```javaScript
export function add(a, b) {
  return a + b;
}
```

Now let's create a file with a unit test in. Named `add.test.js` after the
`add.js` file it is testing also within the `src/` folder:  

**add.test.js**
```javaScript
import { add } from './add'

describe('add', () => {
  it('should add two numbers', () => {
    expect(add(1, 2)).toBe(3);
  });
});
```

### The 'it' keyword
The `it` keyword wraps a single unit test. Each time an `it` is encountered it
will be treated as a new test.

### The 'describe' keyword
We can use `describe` to describe, nest and organise our tests. You can have a
describe nested inside another describe e.g.
```javaScript
describe('add', () => {
  describe('integers', () => {
    it('should add two positive numbers', () => {
      expect(add(1, 2)).toBe(3);
    });

    it('should add two negative numbers', () => {
      expect(add(-1, -2)).toBe(-3);
    });
  });

  describe('strings', () => {
    it('should add two strings', () => {
      expect(add('hello', ' world')).toBe('hello world');
    });
  });
});
```

We can run the test we wrote with the following command:
```
$ npm test
```

We have our first passing unit test!

The process will also continue running as we make changes to the code so we can
check back and see if the tests are passing at any point.

## Chai
Chai provides chain-able language extensions to the JavaScript that you can
using in your assertion statements where you are checking the result of you
test.

It's main purpose is to make your tests read more like sentences. This makes
the tests easier for less technical team members or stake-holders to understand.

It gives you two BDD (Behaviour Driven Development) options for how you
structure your assertions called **expect** and **should**.

Some examples of assertions using **expect** are:
```javaScript
expect(result).to.be.a('string');
expect(result).to.equal('hello')
expect(result).to.equal(2);
```

The same examples using **should** are:
```javaScript
result.should.be.a('string');
result.should.equal('hello');
result.should.equal(2);
```

They provide almost exactly the same functionality ([should has some minor limitations](http://www.chaijs.com/guide/styles/)) so it's really just down to
personal preference. We'll use **expect** for the examples in this session.

### Install Chai
Add Chai to you project by running the following
```
$ npm install --save-dev chai
```

### Use Chai expect in the unit test
Update the `add.test.js` file to import and use Chai expect:

**add.test.js**
```javaScript
import { expect } from 'chai';
import { add } from './add'

describe('add', () => {
  it('should add two numbers', () => {
    expect(add(1, 2)).to.equal(3);
  });
});
```

Check the Jest test runner in your terminal and you'll see the test still
passes.

## Enzyme
```
$ npm install --save-dev enzyme enzyme-adapter-react-16
```

### shallow
TODO explain

Let's create a new file called `App.test.js` in the `src/components` folder to
test the `App.js` component.

**App.test.js**
```javaScript
import React from 'react';
import { expect } from 'chai';
import { shallow } from 'enzyme';
import App from './App';

it('App renders without crashing', () => {
  const component = shallow(<App />);
  expect(component.exists()).to.equal(true);
});
```

### mount

<a name="further"></a>
## Further reading
[Chai website](http://www.chaijs.com/)  
[Enzyme website](http://airbnb.io/enzyme/)  
[Jest website](https://jestjs.io/)  
[TDD in React tutorial (uses Mocha not Jest)](https://daveceddia.com/getting-started-with-tdd-in-react/)  
