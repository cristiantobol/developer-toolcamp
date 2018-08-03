# Introduction to React

* [What is React?](#react)
* [What is Material UI?](#material-ui)
* [Further reading](#further)

## Session Objective
This session will give you an introduction to React in JavaScript. We will build
a React application which talks to the REST API we created and displays the data
from it.

<a name="react"></a>
## What is React?

<a name="material-ui"></a>
## What is Material UI?

## CSS and where to store it.
Explain different approaches available.
Explain it's all been pre-built for app but need to use same id's

## Explanation of all the files already in the project

## Add a title
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
