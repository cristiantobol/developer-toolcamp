# Node Package Manager (NPM)

* [What is Lodash?](#lodash)
* [Using Lodash](#usinglodash)
* [What is Moment.js?](#moment)
* [Using Moment.js](#usingmoment)
* [Formatting dates with Moment.js](#formattinmg)
* [Further reading](#further)

## Session Objective
This session will cover the following:

Finding and working with NPM packages

**Hands on session:**
Using Lodash for common tasks
Using Moment to format dates

<a name="lodash"></a>
## What is Lodash?

Lodash is an npm package that is packed full of useful functions and commands that make working with objects and arrays really simple.  

There are many benefits of using a well supported package:

A well developed library generally has a well supported and active community.
Comprehensive unit tests, which builds confidence in the reliability of the package.
Continuous updates, releasing improvements and bug fixes.

Head over to the NPM page for Lodash:
https://www.npmjs.com/package/lodash

<img src="./resources/session_07_lodash.png" alt="Lodash NPM page" />

The more users, means more ‘eyes on’ to find bugs and help fix issues. Generally, a package with a great deal of activity on NPM is a good sign.  E.g. Weekly downloads.  In the case of Lodash, there seems to be significant weekly downloads and activity.

To Install Lodash, in a terminal type the following command:

```
$ npm install –save lodash
```

Following installation, take a look in package.json file and you hould now see that Lodash is installed as a dependency.

```
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
Moment takes the hassle out of formatting date and is widely used.

*“Parse, validate, manipulate, and display dates and times in JavaScript.”*

1. Head over to npm to confirm the installation instructions and install Moment.js as a dev dependency.

1. Then confirm that moment is installed in the devDependencies of package.json.

```
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

Now that we have moment.js installed, we will use Moment.js to format a “dateCreated” field that can be used to display on each item.

We will make the following changes to our application
* Add the dateAdded field to the RecipeGridList component.
* Add the dateAdded field to the RecipeTile component.
* Add the dateAdded field to the RecipeDetails component.
* Format the date in a friendly way for the tile and the details components.

1. Open the RecipeGridList component.  Add the new dateAdded field as a prop which is passed down to the RecipeTile component.

```
<RecipeTile
              key={tile.id}
              title={tile.title}
              image={tile.image}
              difficulty={tile.difficulty}
              dateAdded={tile.dateAdded}
              onClick={() => props.onClick(tile.id)}
            />
```

2. Open the RecipeTile component.  Add the dateAdded field to the subtitle:

```
<GridListTileBar
          title={this.props.title}
          subtitle={<div><span>Difficulty: {this.props.difficulty}</span>&nbsp;&nbsp;<span>Date added: {this.props.dateAdded}</span></div>}
          actionIcon={
            <IconButton className={classes.icon}>
              <InfoIcon />
            </IconButton>
          }
        />
```

<a name="dateformatting"></a>
## Formatting dates with Moment.js

The dateAdded field in RecipeTile component is an iso8601 formatted date. 

Import moment into the RecipeTile component:

`import moment from 'moment';`

```
moment(new Date(this.props.dateAdded)).format("DD-MMM-YYYY")
```


<a name="further"></a>
## Further reading
[The Lodash module on NPM](https://www.npmjs.com/package/lodash)  
[The Moment module on NPM](https://www.npmjs.com/package/moment)  

