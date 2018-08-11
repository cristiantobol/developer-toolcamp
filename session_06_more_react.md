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
Log to the console to begin with

Handle error with console log too

## Store the recipe data in the App component state
Explain component state

## Display multiple tiles
Store the response in component state
Use a map to create tiles from state with just image initially
Explain map

## Add the props to display the correct recipe image

## Add the props to display the correct title and difficulty
Get trainees to try first.

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

[Promise Documentation]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
