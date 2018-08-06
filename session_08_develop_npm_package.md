# Developing a Node package

* [Overview](#overview)
* [How to create an NPM package](#how)
* [Create the Header application](#create)
* [Configure packages the header app](#configure)
* [Create the component for the header](#header)
* [Clone the React Seed Project which will consume the header](#clone)
* [Further reading](#further)

## Session Objective
This session will cover the following:

Anatomy of an NPM package

**Hands on session:**
* Creating a package
* Cloning the React Seed Project
* Using the package in the React Seed Project
* Including a package from a Github branch and a Github Pull Request

<a name="overview"></a>
## Overview
As you have already seen, there are a multitude of packages freely available to use on NPM. This session will walk through the process to create an NPM package that can be used in the application.

For the purposes of this session, we will create an NPM package that will be responsible for the creating the header of an application.

<a name="how"></a>
## How to create an NPM Package

To create a NPM package, you have to do two things:

1. Create an app containing component
1. Use the component in your app

It really is as simple as that.

<a name="create"></a>
## Create the Header application

1. In IBM Github, create a new repository called dev-toolcamp-header and initialise it with a blank readme file.

1. Clone the repo to a folder on your laptop.

1. Open the project in VS Code

1. Switch to the terminal and navigate to the folder of the new repo.  Type the following command:

```
$ npm init
```

1. Accept all of the default values.

1. Open the header package in VS Code.  
 
1. In VS Code, take a look at the package.json file that has just been initialised.  

<a name="configure"></a>
## Configure packages the header app

1. In the dev-toolcamp-ui package.json file, copy the dependencies and devDependencies sections and paste them into the package.json file of the header app.

```
"dependencies": {
    "@material-ui/core": "^1.3.1",
    "npm": "^6.1.0",
    "react": "^16.4.1",
    "react-dom": "^16.4.1"
  },
  "devDependencies": {
    "react-scripts": "^1.1.4"
  }
```
1. Switch to the terminal and navigate to the dev-toolcamp-header folder and run the following command to install the packages:

```
$npm install
```

1. Add a `.gitignore` file.

1. Click into the `.gitignore` file and type `“node_modules”`.  This will make sure that the node_modules folder is not added to the git repository.

<a name="header"></a>
## Create the component for the header

1. In the header project create a new folder called “src”.  Then create a new file called `src/header.js`.

1. Add the following code to the header.js file:

```
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

1. Push the code to the dev-toolcamp-header repository.

<a name="consume"></a>
## Clone the React Seed Project which will consume the header

1. In the terminal navigate to your root `git` folder.

2. Clone the React Seed Project:

```
git clone git@github.ibm.com:Chris-Dalby-CIC-UK/react-seed-project.git
```

3. Navigate into the React Seed Project folder `cd react-seed-project`.

4. Install the project `npm install`.

<a href="addheader"></a>
## Add the header to the React Seed Project

1. Open the React Seed Project in VSCode.

1. Navigate to `package.json` and add the following in the `dependences` section:

```
"dev-toolcamp-header": "git+ssh://git@github.ibm.com:Chris-Dalby-CIC-UK/dev-toolcamp-header#master",
```

1. Expand the following folder structure for editing `src/MyComponent/MyComponent.js`

1. Import the Header and then add the <Header /> component as below:

```
import React from 'react';
import './MyComponent.css';
import Header from 'dev-toolcamp-header';

const MyComponent = () => (
  <div className="my-component">
    <Header />
    <h1>The React Seed Project</h1>
    <h2>Hello, World</h2>
  </div>
);

export default MyComponent;
```
1. Run `npm install` to add the new component

1. Test the project by starting in dev mode:

```
npm run dev
```
<a name="further"></a>
## Further reading
[Webpack](https://webpack.js.org/)
[React Seed Project](https://github.ibm.com/Chris-Dalby-CIC-UK/react-seed-project)
[How to create a React Component and publish to NPM](https://medium.com/@BrodaNoel/how-to-create-a-react-component-and-publish-it-in-npm-668ad7d363ce)
[Setting up Webpack for React](https://robots.thoughtbot.com/setting-up-webpack-for-react-and-hot-module-replacement)
[Dev Toolcamp Header](https://github.ibm.com/Chris-Dalby-CIC-UK/dev-toolcamp-header)