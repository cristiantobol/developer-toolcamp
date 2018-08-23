# Developing a Node package

* [Overview](#overview)
* [How to create an NPM package](#how)
* [Fork the Header repo](#fork)
* [Clone the Header repo](#clone)
* [Checkout the stage-1 branch](#checkout)
* [Create the files needed for the Header component](#create)
* [Create the component for the header](#header)
* [Clone the React Seed Project which will consume the header](#consume)
* [Install the React Seed Project](#install)
* [Add the header package to the React Seed Project](#add-header)
* [Exercise - Add a Material-UI element](#exercise)
* [Further reading](#further)

## Session Objective
This session will cover the following:

Anatomy of an NPM package
* Creating a package
* Cloning the React Seed Project
* Using the package in the React Seed Project 
* Including a package from a Github branch

<a name="overview"></a>
## Overview
As you have already seen, there are a multitude of packages freely available to use on NPM. This session will walk through the process to create an NPM package that can be used in an application.

For the purposes of this session, we will create an NPM package that will be responsible for creating a header component that can be used in an application.

You will then clone the [React Seed Project](https://github.ibm.com/Chris-Dalby-CIC-UK/react-seed-project) and consume the new header project.

<a name="how"></a>
## How to create an NPM Package
To create a NPM package, you have to do two things:

1. Create an app containing component
1. Use the component in your app

It really is as simple as that.

<a name="fork"></a>
## Fork the Header starting repository
A Header starter project has been created for you.

We will first fork the Header repository we want to work with. This is so we
can make updates to our own copy of it without affecting the baseline version
used by everyone following this session.

Go to https://github.ibm.com/CIC-UK/developer-toolcamp-header and click on the
fork button in the top right hand corner.

If you're given any choice of where to fork to, use your default GitHub account.

<a name="clone"></a>
## Clone the Header starting repository
In the forked repository click `clone or download` and ensuring it says `Clone with SSH` copy the path displayed.

Go to the folder you want to clone the repository folder into. then run:
```
$ git clone <paste path from forked repo>
```

<a name="checkout"></a>
## Checkout the stage-1 branch
To ensure we all start from the same baseline we will now checkout a branch within your developer-toolcamp-header repository.

Checkout the stage-1 branch:
```
$ git checkout stage-1
```

<a name="create"></a>
## Create the files needed for the Header component
1. Add a `.gitignore` file.

2. Click into the `.gitignore` file and type `“node_modules”`.  This will make sure that the node_modules folder is not added to the git repository.

<a name="header"></a>
## Create the component for the header
1. In the header project create a new file called `index.js`.

1. Add the following code to the index.js file:
```javascript
import React from 'react';
class Header extends React.Component {
  render() {
    return (
      <div>This is the really cool header</div>
    );
  }
}
export default Header;
```

1. Push the code to your developer-toolcamp-header repository.

<a name="consume"></a>
## Clone the React Seed Project which will consume the header
1. In the terminal navigate to your root `git` folder.

2. Clone the React Seed Project:
```
$ git clone git@github.ibm.com:CIC-UK/react-seed-project.git
```

<a name="install"></a>
## Install the React Seed Project
1. In the terminal, navigate into the React Seed Project folder.

2. To install the React Seed Project, in the terminal type:
```
$ npm install
```

<a href="add-header"></a>
## Add the header package to the React Seed Project
1. Open the React Seed Project in VSCode.

2. Navigate to `package.json` and add the following in the `dependences` section:
```json
"developer-toolcamp-header": "git+ssh://git@github.ibm.com:<YOUR_GITHUB>/developer-toolcamp-header#stage-1",
```
3. Replace `<YOUR_GITHUB>` in the git repo url above with the name of your git account.

4. Expand the following folder structure for editing `src/MyComponent/MyComponent.js`

5. Import the Header and then add the `<Header />` component as below:
```javascript
import React from 'react';
import Header from 'developer-toolcamp-header';

import './MyComponent.css';

const MyComponent = () => (
  <div className="my-component">
    <Header />
    <h1>The React Seed Project</h1>
    <h2>Hello, World</h2>
  </div>
);

export default MyComponent;
```

1. Run `$ npm install` to add the new component

2. Test the project by starting in dev mode:
```
$ npm run dev
```

3. Open a browser and view the React Seed Project to see the header incorporated:
http://localhost:8080

<a name="exercise"></a>
## Exercise - Add a Material-UI element
Your task is to use Material-UI to add some visual elements to the new header package.

* [Add an AppBar](https://material-ui.com/demos/app-bar/)  
* [Add a Menu to the AppBar](https://material-ui.com/demos/menus/)  
* [Add a button to the AppBar](https://material-ui.com/demos/buttons/)  

<a name="further"></a>
## Further reading
[Webpack](https://webpack.js.org/)  
[React Seed Project](https://github.ibm.com/Chris-Dalby-CIC-UK/react-seed-project)  
[How to create a React Component and publish to NPM](https://medium.com/@BrodaNoel/how-to-create-a-react-component-and-publish-it-in-npm-668ad7d363ce)  
[Setting up Webpack for React](https://robots.thoughtbot.com/setting-up-webpack-for-react-and-hot-module-replacement)  
[Dev Toolcamp Header](https://github.ibm.com/CIC-UK/developer-toolcamp-header)  
[NPM Documentation to install a package](https://docs.npmjs.com/cli/install)  