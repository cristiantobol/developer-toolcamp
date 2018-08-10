# Introduction to React

* [What is React?](#react)
* [What is Material UI?](#material-ui)
* [Further reading](#further)

## Session Objective
This session will give you an introduction to using React in your JavaScript. We
will build a React application which communicates with the REST API we created
in the last session and displays data from it.

<a name="react"></a>
## What is React?
Talk about JSX

<a name="material-ui"></a>
## What is Material UI?

## What are we building?

## Fork the repository

## Clone the repository

## Explanation of all the files already in the project
* `public/index.html`  
The entry point for the application.
Sets the title on the browser window.
Provides a div with id "root" that we can reference and build the application within.  

* `src/index.js`  
Connects the App wrapper imported from `App.jsx` to the div with id "root" from
`index.html`.

* `src/components/App.jsx`
App is the wrapper for our application. We will nest all the React code we
write within this component.

* `src/components/App.css`
This contains some CSS used to style the App code. We import it into App.jsx and reference it later in this tutorial.

* `.gitignore`  
Contains a list of all the files we don't want Git to include in the Git
repository.

* `package.json`  
Defines which dependencies to install when we run `npm install` and how to start
the application when we call `npm start`.

## CSS and where to store it.
Explain different approaches available.
inline vs separate file.
BEM
etc.
Explain it's all been pre-built for app but need to use same id's

## Install and run the application.
Within the repository folder that you've cloned run the following to install all
required dependencies:
```
$ npm install
```

Once the install process finishes run the following to start the application
running:
```
$ npm start
```

You should see a new tab automatically appear in your browser but if it doesn't
you can navigate to http://localhost:3000/ to see the application running on
your machine.

## Add a title
Currently the application doesn't look very exciting. It just displays the words
"Developer toolcamp UI". We're going to add a title using some components from
the material-ui package.  

First of all we need to install material-ui. We can do this by running:
```
$ npm install --save @material-ui/core
```

We're going to use the AppBar from material UI so we will import it and add the
component using JSX syntax.

Add the following import to the existing imports at the top of the file:
```javaScript
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
```

Now replace the following existing code:
```javaScript
<div>
  Developer toolcamp UI
</div>
```

With the App bar code:
```javaScript
<div>
  <AppBar position="static">
    <Toolbar>
    </Toolbar>
  </AppBar>
</div>
```

Your `App.jsx` file should now look like:

**App.jsx**
```javaScript
// 3rd Party
import React from 'react';
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';

// Styling
import './App.css';

class App extends React.Component {

  render() {

    return (
      <div>
        <AppBar position="static">
          <Toolbar>
          </Toolbar>
        </AppBar>
      </div>
    );
  }
}

export default App;
```

Have a look at the running application. It will have automatically updated to
show the changes you've made. You should now see an app bar across the top
of the page.

We'd like to display a title on there so we'll use another material ui component
called Typography to add the word _Recipes_.

Add the following import at the top of the file:
```javaScript
import Typography from '@material-ui/core/Typography';
```
And the following code nested inside the `<Toolbar>` component tags:
```javaScript
<Typography>
  Recipes
</Typography>
```

The application should now display the word Recipes which is great but the font
is a bit small and the colour is hard to read on the background. We'll use the
components **props** to fix that.

### Props
Props are arbitrary inputs provided to React components. They are always read
only and are defined by the component itself. When we use a component we can
pass props to alter the way it looks or behaves.  

On the `Typography` component we are going to use two of the props defined for
us called `color` and `variant`. Update your app code to look like the code
below:

```javaScript
<Typography color="inherit" variant="title">
  Recipes
</Typography>
```

Now take a look in the browser again and you'll see the title is much easier to
read and looks like a title now.

We need to use the API documentation for components we import to see what's
available. The docs for Typography can be found
[here](https://material-ui.com/api/typography/).

Your `App.jsx` file should now look like:

**App.jsx**
```javaScript
// 3rd Party
import React from 'react';
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';

// Styling
import './App.css';

class App extends React.Component {

  render() {

    return (
      <div>
        <AppBar>
          <Toolbar>
            <Typography color="inherit" variant="title">
              Recipes
            </Typography>
          </Toolbar>
        </AppBar>
      </div>
    );
  }
}

export default App;
```

## Add the recipe grid
Next we're going to add a grid to hold our recipes. Initially this will just be
one recipe but we'll later expand to read any number of recipes from our REST
API.

We'll be using more material-ui components so we'll import them into the app
now. Copy the following and paste with the other imports at the top of the `App.jsx` file:
```javaScript
import GridList from '@material-ui/core/GridList';
import GridListTile from '@material-ui/core/GridListTile';
import GridListTileBar from '@material-ui/core/GridListTileBar';
```

First of all we'll add a `GridList` component just beneath the closing
`</AppBar>` which will create a grid to hold the recipe tiles.

```javaScript
<GridList cellHeight={180} cols={4}>
</GridList>
```

We've used props again here to set the height that each recipe image will be
limited to (180px) and also to set the number of columns which will define the
number of tiles to display on each row (4).

The grid list is not visible in the App until it's got something in it. So we're
going to add a recipe tile manually, hard-coding the title and the path to the
image.

Place the `GridListTile` code below inside the `<GridList>` tags you just added:
```javaScript
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
```

Take a look at the result in your browser.

Find your own recipe image online and then Right-Click > 'Copy Image Address'
to update the `src` prop of `img`. Update the `title` prop of `GridListTileBar`
to set a new recipe title too.

Your `App.jsx` file should look similar to the one below now but with your own image and title:

**App.jsx**
```javaScript
// 3rd Party
import React from 'react';
import AppBar from '@material-ui/core/AppBar';
import GridList from '@material-ui/core/GridList';
import GridListTile from '@material-ui/core/GridListTile';
import GridListTileBar from '@material-ui/core/GridListTileBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';

// Styling
import './App.css';

class App extends React.Component {

  render() {
    return (
      <div>
        <AppBar position="static">
          <Toolbar>
            <Typography color="inherit" variant="title">
              Recipes
            </Typography>
          </Toolbar>
        </AppBar>
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

# SWITCH TO NEXT BRANCH HERE

## Checkout stage-2 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we're working in.

Add, commit and push any changes you've made:
```
$ git add *
$ git commit -m "code added in stage 1"
```

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

## Refactoring title into a separate component
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
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';

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

## Refactoring recipe grid into a separate component
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
  
    ```javaScript  
    // 3rd Party
    import React from 'react';
    import AppBar from '@material-ui/core/AppBar';
    import Toolbar from '@material-ui/core/Toolbar';
    import Typography from '@material-ui/core/Typography';

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
</details>

## Get data asynchronously from the REST API
Explain request-promise-native
```
$ npm install --save request
$ npm install --save request-promise-native
```
Explain promises
Log to the console to begin with
Handle error with console log too

## Add multiple tiles
Explain component state
Store the response in component state
Use a map to create tiles from state with just image initially
Explain map

## Refactor tile into separate component
Get trainees to have a go first?

## Get trainees to add the props for title and difficulty
## collapsible markdown?
<details>
  <summary>SOLUTION</summary>
  <p>
  Some explanation  

  ```javaScript
  console.log("cheating")
  ```
  </p>
</details>

# SWITCH TO NEXT BRANCH HERE

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
