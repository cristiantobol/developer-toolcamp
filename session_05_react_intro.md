# Introduction to React

* [What is React?](#react)
* [What is Material UI?](#material-ui)
* [What are we building](#what-building)
* [Fork the repository](#fork)
* [Clone the repository](#clone)
* [Explanation of files already in the project](#existing-files)
* [CSS and management approaches](#css)
* [Install and run the application](#install)
* [Add a title](#add-title)
* [Add the recipe grid](#add-grid)
* [Add all the changes you've made to Git](#commit)
* [Further reading](#further)

## Session Objective
This session will give you an introduction to using React in your JavaScript. We
will build a React application which communicates with the REST API we created
in the last session and displays data from it.

<a name="react"></a>
## What is React?
React describes itself as:
> A JavaScript library for building user interfaces.

It allows you to combine JavaScript and HTML into objects called React
Components that can be built dynamically as your application runs.

It creates a virtual-dom to allow it to only re-render the parts of your page
which have changed. This makes it able to handle large amounts of data and still
perform in a responsive way for users.

It's developed and used by Facebook. It's extremely popular and well documented
online with a thriving community.

Here are some snippets about React from the
[React website](https://reactjs.org/):

> Design simple views for each state in your application, and React will
efficiently update and render just the right components when your data changes.

> Build encapsulated components that manage their own state, then compose them
to make complex UIs.

### JSX
We'll also be using the React syntax extension to JavaScript called JSX.

JSX produces React “elements” which are rendered to the DOM.

React with JSX couples the rendering logic with other UI logic like event
handling, state changes and preparing data to display.

> Instead of artificially separating technologies by putting markup and logic in
separate files, React separates concerns with loosely coupled units called
“components” that contain both.

For more information see
[Introducing JSX](https://reactjs.org/docs/introducing-jsx.html) on the React
website.

<a name="material-ui"></a>
## What is Material-UI?
We will be using [Material-UI][Material-UI] heavily in this project to take
advantage of its pre-built components that make it very quick to create UI
objects like grids, tiles, titles and text.

[Material-UI][Material-UI] describes itself as:
> React components that implement Google's Material Design.

[Material Design](https://material.io/design/) sets out a number of rules to
help you make UIs that are intuitive and pleasing to look at.

<a name="what-building"></a>
## What are we building?
At the end of the React sessions in the developer toolcamp we will have built an
application which displays a grid of tiles displaying recipes loaded from a REST
API.

These tiles will be clickable and will take the user to another view that
displays the full information about that recipe.

This will hopefully lay lots of the groundwork you would need to be able to
build applications and dashboards with React on projects in the future.

<a name="fork"></a>
## Fork the repository
Like with the REST API we will fork the repository we want to work with.

Go to https://github.ibm.com/CIC-UK/developer-toolcamp-ui and click on the fork
button in the top right hand corner.

If you're given any choice of where to fork to, use your default GitHub account.

<a name="clone"></a>
## Clone the repository
In the forked repository click "clone or download" and ensuring it says
"Clone with SSH" copy the path displayed.

Go to the folder you want to clone the repository folder into. then run:
```
$ git clone <paste path from forked repo>
```

<a name="existing-files"></a>
## Explanation of files already in the project
Once you've cloned the repository open the folder in the IDE you're using to
view code.

You'll see there is already a number of files in it. Here's a brief description
of what's there:
* `public/index.html`  
This is the entry point for the application that's served to the browser. In our
case it sets the title on the browser window and provides a `div` with the id
`root` that we can reference and build the application within.  

* `src/index.js`  
This connects the `App` component imported from `App.jsx` to the div with id
`root` from `index.html`.

* `src/components/App.jsx`
This file contains a React component called `App`. It is the wrapper for our
application and we will nest all the React code we write within this component.

* `src/components/App.css`
This file contains some CSS used to style the `App` code. We import it into
`App.jsx` and reference it later in this tutorial.

* `.gitignore`  
This is a standard Git file which contains a list of all the files we don't want
Git to include in the Git repository.

* `package.json`  
This defines which dependencies to install when we run `npm install` and how to
start the application when we call `npm start`.

<a name="css"></a>
## CSS and management approaches
We're not going to touch on CSS in any great detail as part of this course. It's
a large topic worthy of its own session.

Some CSS files have been added to the project at various stages in order to get
components styling correctly without adding extra noise to the React session.

It's worth noting that there are several different common approaches to how you
manage your CSS. We've listed some of them here with links to find out more:

* Store all style in one CSS file (often called main.css)
* Store style in separate CSS files named after the component they style. e.g.
`Title.css` would be used to style `Title.jsx`.
* [JSS](https://github.com/cssinjs/jss) - Using JavaScript to express CSS.
  * Material-UI has a utility called
  [withStyles](https://material-ui.com/customization/css-in-js/#api) that
  builds JSS into Material-UI.
* [SASS/SCSS](https://sass-lang.com/) an extension to CSS to let you use
variables, nesting and mixins to better organise your code and make it more
maintainable and re-usable.
* [BEM naming](http://getbem.com/naming/) can be used with one of the other
approaches above.

<a name="install"></a>
## Install and run the application
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

<a name="add-title"></a>
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

The application should now display the word Recipes which is what we wanted.
However the font is a bit small and the colour is hard to read on the
background. We'll use the components **props** to fix that.

### Props
Props are arbitrary inputs provided to React components. They are always
read-only and are defined by the component itself. When we use a component we
can pass props to alter the way it looks or behaves.  

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

More information about props is available from the
[React website](https://reactjs.org/docs/components-and-props.html)

<a name="add-grid"></a>
## Add the recipe grid
Next we're going to add a grid to hold our recipes. Initially this will just be
one recipe but we'll later expand to read any number of recipes from our REST
API.

We'll be using more material-ui components so we'll import them into the app
now. Copy the following and paste with the other imports at the top of the
`App.jsx` file:
```javaScript
import GridList from '@material-ui/core/GridList';
import GridListTile from '@material-ui/core/GridListTile';
import GridListTileBar from '@material-ui/core/GridListTileBar';
```

First of all we'll add a `GridList` component just beneath the closing
`</AppBar>` which will create a grid to hold the recipe tiles:
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

<a name="commit"></a>
## Add all the changes you've made to Git
We'll now back-up all the changes we've made to our forked copy of the
developer-toolcamp-ui.

Add, commit and push any changes you've made:
```
$ git add *
$ git commit -m "code added in stage 1"
```

In the next session we'll continue our work on this application from a new Git
branch so don't worry if you weren't able to get your application working at the
end of this session.

<a name="further"></a>
## Further reading
The React website has loads of great docs and tutorials.
Some relevant ones for this session are:  
[Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)  
[React components and props](https://reactjs.org/docs/components-and-props.html)  

It's also worth looking at the components and demoes available on material-ui:
[Material-UI][Material-UI]

[Material-UI]: https://material-ui.com/
