# Unit testing

* [What is a unit test?](#unit-test)
* [Jest](#jest)
* [Chai](#chai)
* [Enzyme](#enzyme)
* [Code coverage](#coverage)
* [Possible extensions](#extensions)
* [Further reading](#further)

## Session Objective
This session will give an introduction to unit testing and will specifically
focus on unit testing React components. We will setup and use a number of the
standard unit testing libraries to test our recipes application code.

<a name="unit-test"></a>
## What is a unit test?
Unit testing is the software development practice of aiming to the test the
smallest part of your application in isolation (called a unit) in an individual
and independent way to make sure it is operating properly.

Unit testing is usually automated so that we can run all of our tests in one go
and we can trigger them to run on events like developers committing code to git.

They provide a health-check for the application to tell us whether things are
working or not. Any failing tests are a sign that something in the code needs
attention and they should be addressed and fixed as soon as possible.

Benefits of unit testing:
* We're forced to write code that is testable. Which leads to us writing code
that is de-coupled and modular.
* We can make changes to existing code with more confidence as to whether our
changes have broken any of the existing functionality.
* They can be self-documenting, by which we mean that they provide examples for
other developers on how the code is expected to be used.
* We can use the outcome of the tests in our automation pipelines. For example
we might stop a pull request from being able to be merged if tests aren't all
passing.
* When combined with metrics like [code coverage](#coverage) (covered later) they provide an
indication of the code quality to other developers. Would you chose to import
the 3rd party package with _92% coverage and all tests passing_ or the one with
_45% coverage and 2 tests failing_?

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

Update your scripts section to look like this:
**package.json**
```
"scripts": {
  "start": "react-scripts start",
  "test": "react-scripts test --env=jsdom"
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
Enzyme is a JavaScript testing utility specifically built for React. It is
developed by **airbnb**.

Enzyme offers multiple ways to render your component in order to test it. You
can use shallow rendering or full rendering (mounting).

### Shallow rendering
Explanation from the [shallow rendering API](https://airbnb.io/enzyme/docs/api/shallow.html):
> Shallow rendering is useful to constrain yourself to testing a component as a
unit, and to ensure that your tests aren't indirectly asserting on behavior of
child components.

### Full rendering (mount)
Explanation from the [full rendering API](https://airbnb.io/enzyme/docs/api/mount.html):
> Full DOM rendering is ideal for use cases where you have components that may
interact with DOM APIs or need to test components that are wrapped in higher
order components.

Tests using **Full DOM rendering** require a full DOM API be available. Which
means they need to run in an environment that at least “looks like” a browser
environment.

> The recommended approach to using `mount` is to depend on a library called
`jsdom`  which is essentially a headless browser implemented completely in
JavaScript.

**Note:** Jest actually ships with `jsdom` so we've already got it installed and
ready.

### Shallow rendering vs full rendering
Shallow rendering will only render the components within the render method of
the component you're using. Whereas full rendering will render all of the
components all the way down the tree.

Let's take an example from the Recipes application to compare the two:
```javaScript
import { shallow, mount } from 'enzyme';
import RecipeGridList from './RecipeGridList';

it('shallow renders without errors', () => {
  const component = shallow(<RecipeGridList />);
});

it('full renders without errors', () => {
  const component = mount(<RecipeGridList />);
});
```
In the shallow test we will render the following components:
```
RecipeGridList
└─┬ GridList
  └── RecipeTile
```
In the mount test we will render all components beneath `RecipeGridList`:
```
RecipeGridList
└─┬ GridList
  └─┬ RecipeTile
    └─┬ GridListTile
      └── img
      └─┬ GridListTileBar
        └── ...
```

Shallow rendering is quicker and still allows you to check interactions with the
component like click events. It also allows you to test a smaller unit of your
code.

With full rendering you can test components interacting with each other.

### Rule of thumb
Here's a rule of thumb to give some guidance on when to use shallow and when to
use mount:
1. Always start out using `shallow` until your test requires more.
1. If you want to test the behaviour of the components children use `mount`
1. If you want to update props after creating the component use `mount`

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

Here we have checked that we can render the App without any errors occurring. If
errors did occur we would probably not reach the second line of the test which
checks that the component exists after it has been rendered.

This is a really good test to add as a starting point for every React component
you create as it will quickly cover the majority of code in your application and
provide a basic safety net to tell you if a change you've made has broken
something.

Next we're going to add a test that interacts with the `RecipeTile` after
rendering it. In this test we're going to check that the `onClick` prop is
called when a user clicks on a tile:
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

We're checking that the change has happened by creating a variable called
`changed` which is initially set to false. We then create a function which sets
changed to `true` when the `onClick` prop is called. We then use the `...`
spread operator to expand our props object into separate arguments. This is
equivalent to doing:

```javaScript
const component = shallow(<RecipeTile onClick={ changed = true } />);
```

### Use Enzyme mount in unit tests
One thing you can't do with shallow is access or update your props after you've
created the component. So let's add some examples where we use `mount` instead
to check the props we've set and also update the props after creating the
component.

Before we add the next test we're going to update the actual `RecipeTile` code
to add a new id which will let us reference a sub-component within `RecipeTile`.

Add an `id` prop to the `GridListTileBar` sub-component with the value
`"recipe-tile__bar"`:  
**RecipeTile.jsx**
```javaScript
<GridListTileBar
  id="recipe-tile__bar"
  title={this.props.title}
  subtitle={"Difficulty: " + this.props.difficulty}
/>
```

Going back to the test file we made for RecipeTile. Add `mount` to the imports
from `enzyme` and then add the test below inside the `describe` section after
the existing test:  
**RecipeTile.test.jsx**
```javaScript
it('renders the title prop', () => {
  const initialTitle = 'banana';
  const component = mount(<RecipeTile title={initialTitle} />);
  const text = component.find("#recipe-tile__bar").first().text();

  expect(component.props().title).to.equal(initialTitle);
  expect(text.toString().includes(initialTitle));
});
```

This first `mount` test is:
1. Creating a mounted `RecipeTile` with title set to 'banana'.
1. Locating the child component with the id `recipe-tile__bar` we just added and
getting the text of the first component it finds which matches.
1. Checking the title prop value is set to 'banana'.
1. Checking that the text we extracted from the child component includes
'banana' in it somewhere too.

The result of all of that is that we've now verified that when we set the title
prop on the `RecipeTile` we see that title rendered to the user.

We're going to take this a step further and add another test which changes the
title component to something else ('orange') after creating it:

**RecipeTile.test.jsx**
```javaScript
it('updates the rendered title when the title prop changes', () => {
  const initialTitle = 'banana';
  const component = mount(<RecipeTile title={initialTitle} />);  
  const newTitle = 'orange';
  component.setProps({ title: newTitle });
  const text = component.find("#recipe-tile__bar").first().text();

  expect(component.props().title).to.equal(newTitle);
  expect(text.toString().includes(newTitle));
});
```

This test uses the same approach as in the last test but goes on to verify that
when we change the title prop on the `RecipeTile` we see the new title rendered
to the user.

<a name="coverage"></a>
## Code coverage
Code coverage helps to answer the question of how much unit testing is enough
and gives you an indication of the quality of your code currently.

It will measure which lines of code you have touched with your tests and which
ones you haven't and will then give you a % of how much code is covered.

It will also look at individual branches within the code to make sure you are
covering all the different ways the code can be called.

e.g Take the following simple JavaScript function:
```javaScript
function example(isWorking) {
  return isWorking ? 1 : 2;
  // equivalent to:
  // if(isWorking === true) {
  //   return 1;
  // }
  // return 2;
}
```
This has 2 branches. One where we return 1 and one where we return 2. We'll want
to make sure our tests cover both ideally and code coverage will tell us if we
are.

The usual minimum % to aim for is about **80%**. Ideally your coverage is higher
but you have to make a decision about when the costs of adding new tests
outweigh the benefits.

### Setup code coverage
To use code coverage with Jest we're going to add another script "test-cov" to
the `package.json` so that the scripts section looks as follows:
```
"scripts": {
  "start": "react-scripts start",
  "test": "react-scripts test --env=jsdom",
  "test-cov": "react-scripts test --env=jsdom --coverage"
}
```

We have to use a slightly different approach to run this script as we've given
it the custom name of `test-cov`. To run it we use the following:
```
$ npm run-script test-cov
```

The coverage report then outputs to your terminal but it also creates a really
handy HTML output if you can find it! You need to navigate to the following
address within your browser (replacing <your_username> and <path_to_folder> with
where you've cloned the `developer-toolcamp-ui` repository to):
```
/Users/<your_username>/<path_to_folder>/developer-toolcamp-ui/coverage/lcov-report/src/components/index.html
```
Once you've found it you can bookmark it in the browser.

This will allow you to click around your source code and see exactly what is
covered by your tests and what hasn't been touched so it shows you where to
focus your efforts.

<a name="extensions"></a>
## Possible extensions
* Add unit tests to get the code coverage as high as you can for the application
we've developed.

<a name="further"></a>
## Further reading
[Chai website](http://www.chaijs.com/)  
[Enzyme website](http://airbnb.io/enzyme/)  
[Jest website](https://jestjs.io/)  
[TDD in React tutorial (uses Mocha not Jest)](https://daveceddia.com/getting-started-with-tdd-in-react/)  
