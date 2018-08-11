# More React fundamentals

* [Item 1](#item1)
* [Item 2](#item2)

## Session Objective
This session will continue the introduction to React. We will:
* Re-factor the App component we built.
* Update our application to communicate with the REST API we created in a
previous session and display the data returned from it.
* Add a detailed view of each recipe when a recipe is clicked.

## Checkout the stage-2 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we've been working in.

Checkout the stage-2 branch:
```
$ git checkout stage-2
```

## New CSS files
You'll notice that we now have some new CSS files added to the project. We'll
use these to style components we're about to create and import them as we go.

## Refactoring components
> Components let you split the UI into independent, reusable pieces, and think
about each piece in isolation.

So far all the new React code we've written has gone into `App.jsx`. This will
quickly become unmanageable if we continue to build in this way.  

Already we have 2 distinct components the App Title and the Recipe Grid which
are independent of each other and could be used in isolation.  

We're now going to move them into their own components and import them back in
to `App.jsx` to use them. Let's start with the App Title.  

## Refactor the title into a separate component
Create a new file within the `src/components` folder called `TitleBar.jsx`.  

Since we are going to create a React component we need to import React. Add the
following import to `TitleBar.jsx`:
```javaScript
import React from 'react';
```

Create a React class with an empty render method in `TitleBar.jsx`:
```javaScript
export default class TitleBar extends React.Component {
  render() {}
}
```

Now **cut** the following imports from `App.jsx` and paste them in to `TitleBar.jsx`:
```javaScript
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';
```

Also add the import for the TitleBar style to `TitleBar.jsx`:
```javaScript
import './TitleBar.css';
```

Now **cut** the following code from the `App.jsx` render method and paste it in
to the `TitleBar.jsx` render method:
```javaScript
<AppBar position="static">
  <Toolbar>
    <Typography color="inherit" variant="title">
      Recipes
    </Typography>
  </Toolbar>
</AppBar>
```

Finally, import the TitleBar into `App.jsx`:
```javaScript
import TitleBar from './TitleBar';
```

And add `<TitleBar />` in to the `App.jsx` render method.

Your two JSX files should now look similar to the following:

**App.jsx**
```javaScript
// 3rd Party
import React from 'react';
import GridList from '@material-ui/core/GridList';
import GridListTile from '@material-ui/core/GridListTile';
import GridListTileBar from '@material-ui/core/GridListTileBar';

// Custom
import TitleBar from './TitleBar';

// Styling
import './App.css';

class App extends React.Component {

  render() {
    return (
      <div>
        <TitleBar />
        <GridList cellHeight={180} cols={4}>
          <GridListTile className="recipe-tile">
            <img
              src="https://www.onceuponachef.com/images/2017/12/NY-Cheesecake-575x434.jpg"
              alt="New York Cheesecake"
            />
            <GridListTileBar
              title="New York Cheesecake"
              subtitle="Difficulty: 2"
            />
          </GridListTile>
        </GridList>
      </div>
    );
  }
}

export default App;
```

**TitleBar.jsx**
```javaScript
import React from 'react';
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';

// Styling
import './TitleBar.css';

export default class TitleBar extends React.Component {
  render() {
    return (
      <AppBar position="static">
        <Toolbar>
          <Typography color="inherit" variant="title">
            Recipes
          </Typography>
        </Toolbar>
      </AppBar>
    );
  }
}
```

## Refactor the recipe grid into a separate component
We'll now take the same approach for the section between the `<GridList>` tags
in `App.jsx` and we'll create a new `RecipeGridList` component to hold that
code.

Create a new file within the `src/components` folder called
`RecipeGridList.jsx`.  

Have a go at trying to move the code between the `<GridList>` tags in `App.jsx`
to a new `React.Component` class in `RecipeGridList.jsx`. Then update the
`App.jsx` code to import it.

If you get stuck the finished code for each file is included for you below:

<details>
  <summary><b>App.jsx</b></summary>
  <p>
  Refactored code for App.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';

  // Custom
  import RecipeGridList from './RecipeGridList';
  import TitleBar from './TitleBar';

  class App extends React.Component {
    render() {
      return (
        <div>
          <TitleBar />
          <RecipeGridList />
        </div>
      );
    }
  }

  export default App;
  ```
  </p>

</details>

<details>
  <summary><b>RecipeGridList.jsx</b></summary>
  <p>
  Refactored code for RecipeGridList.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';
  import GridList from '@material-ui/core/GridList';
  import GridListTile from '@material-ui/core/GridListTile';
  import GridListTileBar from '@material-ui/core/GridListTileBar';

  // Styling
  import './RecipeGridList.css';

  export default class RecipeGridList extends React.Component {
    render() {
      return (
        <GridList cellHeight={180} cols={4}>
          <GridListTile className="recipe-tile">
            <img
              src="https://www.onceuponachef.com/images/2017/12/NY-Cheesecake-575x434.jpg"
              alt="New York Cheesecake"
            />
            <GridListTileBar
              title="New York Cheesecake"
              subtitle="Difficulty: 2"
            />
          </GridListTile>
        </GridList>
      );
    }
  }
  ```
  </p>

</details>

## Refactor the recipe tile into a separate component
We also need to refactor the recipe tile into it's own component. We only have
one tile at the moment but we'd like to display multiple recipes and re-use the
same code for each.

Create a new file within the `src/components` folder called `RecipeTile.jsx`.

Have a go at trying to move the code between the `<GridListTile>` tags in
`RecipeGridList.jsx` to a new `React.Component` class in `RecipeTile.jsx`. Then update the `RecipeGridList.jsx` code to import it.

If you get stuck the finished code for each file is included for you below:

<details>
  <summary><b>RecipeGridList.jsx</b></summary>
  <p>
  Refactored code for RecipeGridList.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';
  import GridList from '@material-ui/core/GridList';

  // Custom
  import RecipeTile from './RecipeTile';

  // Styling
  import './RecipeGridList.css';

  export default class RecipeGridList extends React.Component {
    render() {
      return (
        <GridList cellHeight={180} cols={4}>
          <RecipeTile />
        </GridList>
      );
    }
  }
  ```
  </p>

</details>

<details>
  <summary><b>RecipeTile.jsx</b></summary>
  <p>
  Refactored code for RecipeTile.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';
  import GridListTile from '@material-ui/core/GridListTile';
  import GridListTileBar from '@material-ui/core/GridListTileBar';

  // Styling
  import './RecipeTile.css';

  export default class RecipeTile extends React.Component {
    render() {
      return (
        <GridListTile className="recipe-tile">
          <img
            src="https://www.onceuponachef.com/images/2017/12/NY-Cheesecake-575x434.jpg"
            alt="New York Cheesecake"
          />
          <GridListTileBar
            title="New York Cheesecake"
            subtitle="Difficulty: 2"
          />
        </GridListTile>
      );
    }
  }
  ```
  </p>

</details>

## Promises
So far we have just 1 recipe tile displaying data that we've hard-coded into
the tile component. But we want to be able to display a tile for each recipe
available from the REST API we built previously.  

When we communicate with a REST API we want to do it asynchronously. This means
our application will not be un-responsive whilst it's waiting for data to come
back, which would provide a bad user-experience.  

In JavaScript we create a method with a `Promise` object to do this.
> instead of immediately returning the final value, the asynchronous method
returns a promise to supply the value at some point in the future.

There is good [Promise documentation][Promise Documentation] available if you
would like to learn more about how they work.  

## Install request-promise-native
We will be using Promises via a library called `request-promise-native`. This
library provides a convenient way of making a call to an endpoint and handling
the response as a Promise.

To use it we need to add 2 new dependencies to our application:
```
$ npm install --save request
$ npm install --save request-promise-native
```

## Get recipe data asynchronously from the REST API
Now import from `request-promise-native` at the top of the `App.jsx` file:
```javaScript
import request from 'request-promise-native';
```

### Create the getRecipeData method

Within the App class we just have one method at the moment called `render`.
We're going to add another called `getRecipeData` with the following code:
```javaScript
getRecipeData() {
  const options = {
    uri: 'http://localhost:9000/recipes',
    json: true,
  };

  request(options)
    .then((recipes) => {console.log(recipes)})
    .catch((err) => {console.log(`Error getting recipes ${err}`)});
}
```
The `options` variable sets the address we want to access (which is the address
of our REST API). It also specifies that we would like the response in JSON
format.

The `request` from `request-promise-native` then sends a request with these
options. This returns a `Promise` object which we chain functions to with the
`.then` syntax.

The code in `.then` will be triggered when we get a successful response from our
REST API. Inside the `.then` we've used an arrow function to take the response
and store it in a variable called `recipes` and we then print the variable to
the browser console.

We also chained a `.catch` to the Promise which will be triggered when we get an
unsuccessful response. We then log this response to the browser console.

If for example your REST API is not running the log in the console will look
something like: `Error getting recipes RequestError: TypeError: Failed to fetch`
.

### Call the getRecipeData method from the constructor

We've not called this method anywhere yet so we'll add a call to it now. We want
to get this data when the App component is created so we'll add a constructor to
it so we can call it in there. Add another method to the App class called
`constructor` with the following code:
```javaScript
constructor(props) {
  super(props);

  this.getRecipeData();
}
```

By default we don't need to create a component for a React Component unless we
need to add something to it. In order to preserve the existing behaviour we have
to add an argument called `props` and pass it to the parent of the `App` class
which will be the `React.Component` class using the `super` keyword.

We've then added a call to the `getRecipeData` method within the constructor
too. We have to prefix it with `this.` because it's a method of the same class.

Now go to the application running in your browser and open the console by
pressing the `alt cmd j` keys.

You'll see a log like `> (6) [{…}, {…}, {…}, {…}, {…}, {…}]`. Click the arrow
to inspect the object and verify it matches the data you see when you visit the
REST API at http://localhost:9000/recipes.

So we've now managed to access data from our REST API but we've not displayed
anything from it yet.

## Store the recipe data in the App component state
We need to start using a concept in React called `state` in order to achieve
this. State is similar to `props` that we encountered earlier, but it is private and fully controlled by the component.

Every time the state is updated the component will automatically re-render.

A more in depth example of component state is available on the
[React website](https://reactjs.org/docs/state-and-lifecycle.html).

We can access the state through `this.state`. We also define the initial state
in the constructor using `this.state`. However we have to use `this.setState`
if we want to modify it anywhere outside the constructor.

Update the `constructor` method so that it matches the code below:
```javaScript
constructor(props) {
  super(props);

  this.state = {
    recipes: [],
  };

  this.getRecipeData = this.getRecipeData.bind(this);

  this.getRecipeData();
}
```

Here we've created a `recipes` key in the initial state and set it's value to an
empty array, because we don't have any recipes yet.

We've also added a bind statement to bind `this` to the `getRecipeData` method.
The purpose of this line is that it gives us access to the class instance inside
the `getRecipeData` method, which we need in order to update the component state
when we receive the recipes.

Update the `.then` function of the `getRecipeData` method so that it looks like:
```JavaScript
.then((recipes) => {this.setState({ recipes: recipes })})
```

We're now storing the recipes we receive in the component state instead of
logging them to the console. This means we'll now be able to access them in the
render method and display the data from them in the application.

## Display multiple tiles
We're now going to update the application to display a recipe tile for each
recipe listed in the response.

We'll define a new `prop` called recipes to pass the recipe data from the App
to the RecipeGridList.

We do this by adding the prop to the `App` components `render` method on the
`RecipeGridList` line:
```javaScript
<RecipeGridList recipes={this.state.recipes} />
```
We need to use `{}` around the reference to the state because it is a variable
and we want React to evaluate it to its value at render time.

`RecipeGridList` will now be receiving a new prop called `recipes` but we won't
see any difference because we've not told it to use it yet.

Now in `RecipeGridList.jsx` we're going to replace `<RecipeTile />` with:
```javaScript
{this.props.recipes.map(tile => (<RecipeTile />))}
```

Here we're using a JavaScript map iterator to go through every entry in the
recipes array and create a `RecipeTile` for each entry.

Currently all of the tiles will look the same as we're not actually reading any
information yet from the tile object we get from the map.

For more information about using a map with an Array have a look at the
[MDN Array.prototype.map() docs][Array Map Documentation].

Have a look at the application in the browser and you'll see multiple recipe
tiles all with the same information on them.

## Add the props to display the correct recipe image
Let's update the images on the tiles now to use the images supplied in the REST
API response.

Each recipe in the response has an image key with a url that we can use. First
of all we need to update `RecipeGridList` to pass the image as a prop to the
`RecipeTile`.

In `RecipeGridList.jsx` update the line containing the map to look like:
```javaScript
{this.props.recipes.map(tile => (<RecipeTile image={tile.image}/>))}
```

We're now using some data from the `tile` object in the map and passing it as a
prop called `image` to `RecipeTile`.

Next we need to update `RecipeTile` to use the prop instead of the hard-coded
URL it has at the moment.

In `RecipeTile.jsx` update the `img` component to look like:
```javaScript
<img
  src={this.props.image}
  alt="New York Cheesecake"
/>
```

Take a look at the application in the browser and you'll now see multiple recipe
tiles with different images. The title and difficulty still needs updating
though.

## Add the props to display the correct title and difficulty
Have a go at updating the title and difficulty from the information returned
from the REST API.

You will need to update the `RecipeGridList.jsx` and `RecipeTile.jsx` files.

The fields are called `title` and `difficulty` in the recipe data.

If you get stuck the finished code for each file is included for you below. The
`App.jsx` won't need updating but it's included for reference too:

<details>
  <summary><b>App.jsx</b></summary>
  <p>
  Existing code for App.jsx:

  ```javaScript
  import React from 'react';
  import request from 'request-promise-native';

  // Custom
  import RecipeGridList from './RecipeGridList';
  import TitleBar from './TitleBar';

  class App extends React.Component {
    constructor(props) {
      super(props);

      this.state = {
        recipes: [],
      };

      this.getRecipeData = this.getRecipeData.bind(this);

      this.getRecipeData();
    }

    getRecipeData() {
      const options = {
        uri: 'http://localhost:9000/recipes',
        json: true,
      };

      request(options)
        .then((recipes) => {this.setState({ recipes: recipes })})
        .catch((err) => {console.log(`Error getting recipes ${err}`);});
    }

    render() {
      return (
        <div>
          <TitleBar />
          <RecipeGridList recipes={this.state.recipes} />
        </div>
      );
    }
  }

  export default App;
  ```
  </p>

</details>

<details>
  <summary><b>RecipeGridList.jsx</b></summary>
  <p>
  Updated code for RecipeGridList.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';
  import GridList from '@material-ui/core/GridList';

  // Custom
  import RecipeTile from './RecipeTile';

  // Styling
  import './RecipeGridList.css';

  export default class RecipeGridList extends React.Component {
    render() {
      return (
        <GridList cellHeight={180} cols={4}>
          {this.props.recipes.map(tile => (
            <RecipeTile
              difficulty={tile.difficulty}
              image={tile.image}
              title={tile.title}
            />
          ))}
        </GridList>
      );
    }
  }
  ```
  </p>

</details>

<details>
  <summary><b>RecipeTile.jsx</b></summary>
  <p>
  Updated code for RecipeTile.jsx:

  ```javaScript
  // 3rd Party
  import React from 'react';
  import GridListTile from '@material-ui/core/GridListTile';
  import GridListTileBar from '@material-ui/core/GridListTileBar';

  // Styling
  import './RecipeTile.css';

  export default class RecipeTile extends React.Component {
    render() {
      return (
        <GridListTile className="recipe-tile">
          <img
              src={this.props.image}
              alt={this.props.title}
          />
          <GridListTileBar
            title={this.props.title}
            subtitle={"Difficulty: " + this.props.difficulty}
          />
        </GridListTile>
      );
    }
  }
  ```
  </p>

</details>

Congratulations you now have a completed display dashboard!

## Add all the changes you've made to Git
We'll now back-up all the changes we've made to our forked copy of the
developer-toolcamp-ui.

Add, commit and push any changes you've made:
```
$ git add *
$ git commit -m "code added in stage 2"
```

We'll now continue our work on this application from a new Git branch so don't worry if you weren't able to get your application working at this point.

## Checkout the stage-3 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we've been working in.

Checkout the stage-3 branch:
```
$ git checkout stage-3
```

## Add recipe details page with recipe title

## Add state to manage which page we're on.
Add state
Add render decision based on state

## Add click event to tile to display details
Explain click -> onRecipeClick -> onTileSelected
Explain about keeping components dumb.

## Add click event to title bar to return to dashboard
Update css cursor too (Update classNames "title-bar__title")

## Add ingredients
Create as separate component straight away this time.

## Add method
Copy-paste ingredients
Explain that you could re-use the same component and pass a prop for
whether to add the number and whether to add the divider.
Leave as extension exercise for trainees.

## Add details
Do we want more than difficulty and date added?
Could convert difficulty to star rating or word like Easy, Medium, Hard.
Leave as extension exercise for trainees to do this or add more fields.

<a name="further"></a>
## Further reading
[Promise Documentation][Promise Documentation]
[Array Map Documentation][Array Map Documentation]  

The React website has loads of great docs and tutorials.
Some relevant ones for this session are:  
[React component state](https://reactjs.org/docs/state-and-lifecycle.html)

[Array Map Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
[Promise Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
