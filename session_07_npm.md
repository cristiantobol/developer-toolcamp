# Node Package Manager (NPM)

* [Checkout the stage-4 branch](#stage-4)
* [Finding NPM packages](#npm)
* [What is Lodash?](#lodash)
* [Using Lodash](#usinglodash)
* [What is Moment.js?](#moment)
* [Using Moment.js](#usingmoment)
* [Formatting dates with Moment.js](#dateformatting)
* [Further reading](#further)

## Session Objective
This session will continue the introduction to React and will cover the following:

* Finding and working with NPM packages
* Using Lodash to manipulate arrays and objects
* Using Moment to format dates and times

<a name="stage-4"></a>
## Checkout the stage-4 branch
To ensure we all continue from the same baseline we will now checkout a new
branch within the developer-toolcamp-ui repository we've been working in.

Checkout the stage-4 branch:
```
$ git checkout stage-4
```

<a name="npm"></a>
## About Node Package Manager (NPM)
Applications can make use of advanced functionality by importing packages or modules created by 3rd parties, which can be installed using the Node Package Manager (NPM).  There are many benefits of using a well supported package:

* Comprehensive unit tests, which builds confidence in the reliability of the package
* Continuous updates, releasing improvements and bug fixes
* A well developed library generally has a well supported and active community

Head over to the NPM page for Lodash:
https://www.npmjs.com/package/lodash

<img src="./resources/session_07_lodash.png" alt="Lodash NPM page" />

The more users, means more ‘eyes on’ to find bugs and help fix issues. Generally, a package with a great deal of activity on NPM is a good sign.  E.g. Weekly downloads.  In the case of Lodash, there seems to be significant weekly downloads and activity.

<a name="lodash"></a>
## What is Lodash?

Lodash is an npm package that is packed full of useful functions and commands that make working with objects and arrays really simple.  

To Install Lodash, in a terminal type the following command:
```
$ npm install –save lodash
```

Following installation, take a look in `package.json` file and you hould now see that Lodash is installed as a dependency.
```json
"dependencies": {
    "@material-ui/core": "^1.3.1",
    "@material-ui/icons": "^1.1.0",
    "lodash": "^4.17.10",
    "react": "^16.4.1",
    "react-dom": "^16.4.1"
},
```

<a name="usinglodash"></a>
TODO - Using Lodash to remove properties from an object

<a name="whatismoment"></a>
## What is Moment.js?
Moment takes the hassle out of formatting dates and timestamps and is widely used.

> Parse, validate, manipulate, and display dates and times in JavaScript.

1. Head over to npm to confirm the installation instructions and install Moment.js as a dev dependency.
```
$ npm install --save-dev moment
```

2. Then confirm that moment is installed in the devDependencies of package.json.
```json
"devDependencies": {
    "chai": "^4.1.2",
    "enzyme": "^3.3.0",
    "enzyme-adapter-react-16": "^1.1.1",
    "jest": "^23.2.0",
    "moment": "^2.22.2",
    "react-scripts": "^1.1.4"
}
```

<a name="usingmoment"></a>
## Using Moment.js

Now that we have moment.js installed, we can use it to format a `dateCreated` field that will be display with each recipe.

We will make the following changes to our application
* Add the dateAdded field to the RecipeGridList component.
* Add the dateAdded field to the RecipeTile component.
* Add the dateAdded field to the RecipeDetails component.
* Format the date in a friendly way for the tile and the details components.

1. Open the RecipeGridList component.  Add the new dateAdded field as a prop which is passed down to the RecipeTile component.
```jsx
<RecipeTile
            key={tile._id}
            difficulty={tile.difficulty}
            image={tile.image}
            title={tile.title}
            dateAdded={tile.dateAdded}
            onClick={() => this.props.onRecipeClick(tile._id)}
          />
```

2. Open the RecipeTile component.  Add the dateAdded field to the subtitle:
```jsx
<GridListTile className="recipe-tile" onClick={this.props.onClick}>
  <img
      src={this.props.image}
      alt={this.props.title}
  />
  <GridListTileBar
    title={this.props.title}
    subtitle={<div><span>Difficulty: {this.props.difficulty}</span>&nbsp;&nbsp;<span>Date added: {this.props.dateAdded}</span></div>}
  />
</GridListTile>
```

<a name="dateformatting"></a>
## Formatting dates with Moment.js

The `dateAdded` field in `RecipeTile` component is an iso8601 formatted date, which is often used as a format when saving dates to a database or when passing a date to an online service.  However, it doesn't look very human friendly, so we will format the date to make it easier to read:

1. Import moment into the RecipeTile component:
```javascript
import moment from 'moment';
```

2. Format the date using moment, by replacing `this.props.dateAdded` with the following:

```javascript
moment(new Date(this.props.dateAdded)).format("DD-MMM-YYYY")
```

3. Open the RecipeDetails component.  Add the dateAdded prop to pass down to the RecipeMetaData component:
```javascript
<RecipeMetaData
          dateAdded={recipe.dateAdded}
          difficulty={recipe.difficulty}
        />
```

4. Open the RecipeMetaData component and import moment into the component:
```javascript
import moment from 'moment';
```

5. Add the formatted date to the MetaData component:
```javascript
<List>
  <ListItem key="difficulty">
    <ListItemText primary={"Difficulty: " + props.difficulty} />
  </ListItem>
  <ListItem key="dateAdded">
    <ListItemText primary={"Added: " + moment(new Date(props.dateAdded)).format("DD-MMM-YYYY")} />
  </ListItem>
</List>
```

6. Take a look at the app and you will now see the date formatted correctly and displayed on the tile grid and recipe details pages.

<a name="further"></a>
## Further reading
[The Lodash module on NPM](https://www.npmjs.com/package/lodash)  
[The Moment module on NPM](https://www.npmjs.com/package/moment)  
More details about an [iso8601 formatted date](https://en.wikipedia.org/wiki/ISO_8601)
