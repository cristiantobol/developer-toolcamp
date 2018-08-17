# Unit testing

* [Jest](#jest)
* [Chai](#chai)
* [Enzyme](#enzyme)
* [Further reading](#further)

<a name="jest"></a>
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

<a name="chai"></a>
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

<a name="enzyme"></a>
## Enzyme
TODO explain

### shallow vs mount
TODO explain

### Getting Enzyme set up
Adding enzyme to your project is a bit more involved as it doesn't work with
`react-scripts` out of the box.

We have to add some additional file watching utilities to our Mac first for this
to work with the Sierra OSX.

### Installation
First install [xcode](https://developer.apple.com/xcode/). This is a dependency
for [watchman](https://facebook.github.io/watchman/) that we'll install after
this. Unfortunately xcode isn't installed by homebrew automatically when we do
the watchman install though:
```
$ xcode-select --install
```

Click "Install" in pop-up that opens. It may take about 5 minutes to install.

Next install [watchman](https://facebook.github.io/watchman/) using homebrew:
```
$ brew install watchman
```

Lastly add the required dependencies to your package:
```
$ npm install --save-dev enzyme enzyme-adapter-react-16 react-test-renderer
```

### Setup repository
Now we've finished the installs we need to add a new Jest setup file. Create a
new file in the `src` folder called `setupTests.js`:  

**setupTests.js**
```javaScript
import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });
```
This file is picked up automatically by Jest and adds the adapter for Enzyme to
work with React v16.

We're now ready to start using Enzyme in a test.

### Use Enzyme shallow in a unit test
Let's create a new file called `App.test.jsx` in the `src/components` folder to
test the `App.jsx` component.

**App.test.jsx**
```javaScript
import React from 'react';
import { expect } from 'chai';
import { shallow } from 'enzyme';
import App from './App';

describe('App component', () => {
  it('renders without errors', () => {
    const component = shallow(<App />);
    expect(component.exists()).to.equal(true);
  });
});
```
TODO explain

**RecipeTile.test.jsx**
```javaScript
import React from 'react';
import { expect } from 'chai';
import { shallow } from 'enzyme';
import RecipeTile from './RecipeTile';

describe('RecipeTile component', () => {
  it('calls the onClick prop when it is clicked', () => {
    let changed = false;
    const props = {
      onClick: () => { changed = true }
    }
    const component = shallow(<RecipeTile { ...props } />);
    component.simulate('click')
    expect(changed).to.equal(true);
  });
});
```
TODO explain

### mount
TODO example and explain

<a name="further"></a>
## Further reading
[Chai website](http://www.chaijs.com/)  
[Enzyme website](http://airbnb.io/enzyme/)  
[Jest website](https://jestjs.io/)  
[TDD in React tutorial (uses Mocha not Jest)](https://daveceddia.com/getting-started-with-tdd-in-react/)  
