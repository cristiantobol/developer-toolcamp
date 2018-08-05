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

* `.gitignore`  
Contains a list of all the files we don't want Git to include in the Git
repository.

* `package.json`  
Defines which dependencies to install when we run `npm install` and how to start
the application when we call `npm start`.

## CSS and where to store it.
Explain different approaches available.
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


Explain props  
Add to app.jsx to start with

## Add a grid with 1 tile
Hard-code the values to display at first
Grab image from google on the fly.
Add to app.jsx to start with

## Refactor title and grid into separate components
One for TitleBar
One for RecipeGridList

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
Use a map to create tiles from state
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

## Add recipe details page with recipe title

## Add state to manage which page we're on.
Add state
Add render decision based on state

## Add click event to tile to display details
Explain click -> onRecipeClick -> onTileSelected
Explain about keeping components dumb.

## Add click event to title bar to return to dashboard
Update css cursor too or have it done already?

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
