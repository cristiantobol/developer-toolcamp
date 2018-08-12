# More React fundamentals

* [Checkout the stage-2 branch](#stage-2)
* [New CSS files](#new-css)
* [Refactoring components](#refactor-components)
* [Refactor the title into a separate component](#refactor-title)
* [Refactor the recipe grid into a separate component](#refactor-grid)
* [Refactor the recipe tile into a separate component](#refactor-tile)
* [Promises](#promises)
* [Install request-promise-native](#request-promise-native)
* [Get recipe data asynchronously from the REST API](#get-rest-api)
* [Store the recipe data in the App component state](#data-in-state)
* [Display multiple tiles](#display-multiple)
* [Add the props to display the correct recipe image](#display-image)
* [Add the props to display the correct title and difficulty](#display-title)
* [Add all the changes you've made to Git](#commit-2)
* [Checkout the stage-3 branch](#stage-3)
* [New JSX and CSS files](#new-jsx)
* [Add click event to tile to display details](#click-tile)
* [Add App state to manage which view we're on](#manage-view)
* [Add click event to title bar to return to dashboard](#click-title)
* [Possible extensions](#extensions)
* [Further reading](#further)

## Session Objective
This session will continue the introduction to React. We will:
* Re-factor the App component we built.
* Update our application to communicate with the REST API we created in a
previous session and display the data returned from it.
* Add a detailed view of each recipe when a recipe is clicked.

<a name="stage-2"></a>
## Checkout the stage-2 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we've been working in.

Checkout the stage-2 branch:
```
$ git checkout stage-2
```

<a name="new-css"></a>
## New CSS files
You'll notice that we now have some new CSS files added to the project. We'll
use these to style components we're about to create and import them as we go.

<a name="refactor-components"></a>
## Refactoring components
> Components let you split the UI into independent, reusable pieces, and think
about each piece in isolation.

So far all the new React code we've written has gone into `App.jsx`. This will
quickly become unmanageable if we continue to build in this way.  

Already we have 2 distinct components the App Title and the Recipe Grid which
are independent of each other and could be used in isolation.  

We're now going to move them into their own components and import them back in
to `App.jsx` to use them. Let's start with the App Title.  

<a name="refactor-title"></a>
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

<a name="refactor-grid"></a>
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

<a name="refactor-tile"></a>
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

<a name="promises"></a>
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

<a name="request-promise-native"></a>
## Install request-promise-native
We will be using Promises via a library called `request-promise-native`. This
library provides a convenient way of making a call to an endpoint and handling
the response as a Promise.

To use it we need to add 2 new dependencies to our application:
```
$ npm install --save request
$ npm install --save request-promise-native
```

<a name="get-rest-api"></a>
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

<a name="data-in-state"></a>
## Store the recipe data in the App component state
We need to start using a concept in React called `state` in order to achieve
this. State is similar to `props` that we encountered earlier, but it is private
and fully controlled by the component.

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

<a name="display-multiple"></a>
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

<a name="display-image"></a>
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

<a name="display-title"></a>
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

<a name="commit-2"></a>
## Add all the changes you've made to Git
We'll now back-up all the changes we've made to our forked copy of the
developer-toolcamp-ui.

Add, commit and push any changes you've made:
```
$ git add *
$ git commit -m "code added in stage 2"
```

We'll now continue our work on this application from a new Git branch so don't
worry if you weren't able to get your application working at this point.

<a name="stage-3"></a>
## Checkout the stage-3 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we've been working in.

Checkout the stage-3 branch:
```
$ git checkout stage-3
```

<a name="new-jsx"></a>
## New JSX and CSS files
There are a number of new files added after checking out this new branch.

Due to time constraints we have included a pre-built recipe details page to
display the ingredients, method and meta-data for each recipe.

The new components used to build this page all use the same approaches we have
already seen with information being passed as `props` and a `map` being used to
render a list of items from an Array.

You're encouraged to take a closer look at the following files in your own time
to understand them better:
* `RecipeDetails.jsx`
* `RecipeMetaData.jsx`
* `RecipeMethod.jsx`
* `RecipeIngredients.jsx`

For the next part of this tutorial we will be focusing on navigation between
components, handling click events and presenting the user with different views.

<a name="click-tile"></a>
## Add click event to tile to display details
A `RecipeDetails` component has been pre-built for you but we've not currently
got any way of accessing it.

We're going to set it up so that when we click on a recipe tile we will view the
full details of that recipe.

It's the `RecipeTile` component which will receive the click but we want the
`App` component to make the decision to switch the view. So we will need to pass
the event from the `RecipeTile` to the `RecipeGridList` and on to the `App`.

### Handling the click in RecipeTile
First of all we'll add an `onClick` handler to the `RecipeTile` by adding a new
prop called `onClick`.

Update `RecipeTile.jsx` to add the onClick to the `<GridListTile>` line:
```javaScript
<GridListTile className="recipe-tile" onClick={this.props.onClick}>
```

The `RecipeGridList` is responsible for creating the tiles and knowing which
tile is which. So the tile just needs to say "I've been clicked" and doesn't
need to provide any further information.

It doesn't know what happens when it's clicked. This is all part of keeping the
component as dumb as possible so that it is independent and can be easily
re-used.

### Handling the click in RecipeGridList
The `RecipeGridList` now needs to supply this prop to the `RecipeTile` as it
isn't currently.

Update the `<RecipeTile>` that is created in `RecipeGridList.jsx` so that it
has two additional props `key` and `onClick`:
```javaScript
<RecipeTile
  key={tile._id}
  title={tile.title}
  image={tile.image}
  difficulty={tile.difficulty}
  onClick={() => this.props.onRecipeClick(tile._id)}
/>
```

Here we've used a new key/field on each recipe returned by the REST API called
`_id`. This isn't something that we had set in our initial import data, it was
added by MongoDB when we performed the import, so that each record had a unique
identifier. This is quite handy for us now as we need to be able to uniquely
identify which tile was clicked on.

In the last code change we set the `onClick` prop of the `RecipeTile` to trigger
a prop on the `RecipeGridList` called `onRecipeClick`. This prop we are treating
as a function and we've passed `tile._id` as the first argument. We'll now need
to handle setting `onRecipeClick` in the `App` and we'll see how to access the
unique id there.

We've also used the `tile._id` to set the `key` prop on the `RecipeTile`. React
requests that you use a unique key set in this way every time you have a list
of components. This allows it to be selective about which ones to render and
can improve the performance of you're application. If you don't set you will see
an error in the console but it won't stop the application from working.

### Handling the click in App
So far we've received a click on a `RecipeTile` and we've passed that event to
the `RecipeGridList` and enriched it with information about which tile it was.
We now want to store that information in the `state` of the `App` so that we
can eventually display a page about the recipe that was clicked.

First of all create a method in `App.jsx` which logs the tile that has been
clicked to the browser console:
```javaScript
handleTileSelected(id) {
  console.log("Recipe " + id + " clicked!");
}
```

Now in `App.jsx` set that as the `onRecipeClick` prop for `<RecipeGridList>` in
the render method:
```javaScript
<RecipeGridList recipes={this.state.recipes} onRecipeClick={this.handleTileSelected}/>
```

Click a tile in your browser and see the different IDs being logged.

Now we're going to keep track of the selected recipe in the `state` instead.
First of all we'll update the constructor to:
* add a placeholder for the selected recipe in the initial state
* bind the new method `handleTileSelected` so that we can access `this` inside
it.

Update your constructor to look like:
```javaScript
constructor(props) {
  super(props);

  this.state = {
    recipe: null,
    recipes: [],
  };

  this.getRecipeData = this.getRecipeData.bind(this);
  this.handleTileSelected = this.handleTileSelected.bind(this);

  this.getRecipeData();
}
```
We've initially set `recipe` to `null` because no recipe has been selected when
the application is first loaded.

Now we need to update `handleTileSelected` to find the recipe that has the same
`id` and update the selected recipe in the state:
```javaScript
handleTileSelected(id) {
  const recipe = this.state.recipes.find(tile => tile._id === id);
  this.setState({ recipe: recipe });
}
```
Please see the [MDN Array.prototype.find() docs][Array Find Documentation] for
more information about the `.find` function.

We now have a copy of the selected recipe in the state, ready to use on our
pre-built recipe details page. So the next step is to display it!

<a name="manage-view"></a>
## Add App state to manage which view we're on
In the `constructor` for the `App` add another key called `showDashboard` to the
initial state so that it looks like:
```javaScript
this.state = {
  recipe: null,
  recipes: [],
  showDashboard: true,
};
```

Update the `handleTileSelected` method to set `showDashboard` to `false`,
allowing us to trigger a view change when a tile is clicked:
```javaScript
handleTileSelected(id) {
  const recipe = this.state.recipes.find(tile => tile._id === id);
  this.setState({
    recipe: recipe,
    showDashboard: false,
  });
}
```

Import the pre-built `RecipeDetails` component so that we can use it in the
`render` method:
```javaScript
import RecipeDetails from './RecipeDetails';
```

Update the `render` method to decide which view to show based on whether
`this.state.showDashboard` is set to `true` or `false`:
```javaScript
render() {
  return (
    <div>
      <TitleBar />
      {this.state.showDashboard && (
        <RecipeGridList recipes={this.state.recipes} onRecipeClick={this.handleTileSelected}/>
      )}
      {!this.state.showDashboard && (
        <RecipeDetails recipe={this.state.recipe} />
      )}
    </div>
  );
}
```
When `this.state.showDashboard` evaluates to `true` the `RecipeGridList` will be
rendered. When it evaluates to false the `RecipeDetails` will be shown.

Try clicking on a tile in the application again now and you'll be taken to the
details for that recipe.

<a name="click-title"></a>
## Add click event to title bar to return to dashboard
It's great that we can click on a tile now and view the details, but we have no
way of getting back to the dashboard (unless we refresh the page).

The last thing we'll do is add an event when you click on the "Recipes" word in
the title of the application to take us back to the dashboard.

In `TitleBar.jsx` add a new `onTitleClick` prop which is triggered by clicking
on the `Typography` component. We're also setting the `className` here to pick
up a pre-defined style from `TitleBar.css` which will change the cursor to show
it's clickable when you hover over the title:
```javaScript
render() {
  return (
    <AppBar position="static">
      <Toolbar>
        <Typography
          color="inherit"
          variant="title"
          className="title-bar__title"
          onClick={this.props.onTitleClick}
        >
          Recipes
        </Typography>
      </Toolbar>
    </AppBar>
  );
}
```

In `App.jsx` add a new method called `handleDashBoard` which sets the `App`
state so that the dashboard is showing again and no recipe is selected:
```javaScript
handleDashBoard() {
  this.setState({
    showDashboard: true,
    recipe: null,
  });
}
```

The handleDashBoard method needs to use `this` to set state so make sure you
bind it in the `constructor` of `App` as well:
```javaScript
this.handleDashBoard = this.handleDashBoard.bind(this);
```

In the `render` method of the `App` we now need to connect the `onTitleClick`
prop with the method we've just written:
```javaScript
<TitleBar onTitleClick={this.handleDashBoard} />
```

That's it! Take a look at the application in your browser and you should be able
to navigate around the application freely now!

<a name="extensions"></a>
## Possible extensions
If you'd like to take this project further here are some ideas of things to try:
* Convert the difficulty number to a star rating using icons or a word like Easy,
Medium, Hard.  
* Merge the `RecipeIngredients` and `RecipeMethod` classes into the same
`React.Component` class and then use additonal props to set the title and decide
whether to add a number in front of the list item and whether to display
dividers in-between.  
* Add some more fields to the recipe objects you imported into MongoDB. Then
render them using new props on the existing components in the application.
* Read about [prop-types and default props][Proptypes] and then use them in the
application.
* Create another view in the application for an entry form to create new
recipes. Send these as POST requests to the REST API and see them appear back in
the application.

<a name="further"></a>
## Further reading
The React website has loads of great docs and tutorials.
Some relevant ones for this session are:  
[React component state](https://reactjs.org/docs/state-and-lifecycle.html)

More infomation on some of the JavaScript objects used in this tutorial are
available here:  
[Promise Documentation][Promise Documentation]  
[Array Map Documentation][Array Map Documentation]  
[Array Find Documentation][Array Find Documentation]

Some important concepts we've not had a chance to cover are:  
[Components as a Function vs React.Component vs React.PureComponent](https://reactjs.org/docs/react-api.html)  
[Prop types and default props][Proptypes]  
[Component lifecycle methods](https://medium.com/@baphemot/understanding-reactjs-component-life-cycle-823a640b3e8d)

[Array Map Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
[Array Find Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
[Promise Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[Proptypes]: https://reactjs.org/docs/typechecking-with-proptypes.html
