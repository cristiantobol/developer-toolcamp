# Introduction to Redux

* [What is Redux?](#what)
* [Three principles of Redux](#principles)
* [When do you need Redux?](#when)
* [How does Redux work?](#how)
* [Further reading](#further)

## Session Objective
This session will give an introduction to Redux with React. We will cover the
main concepts of Redux and when to use it. We won't be writing any Redux code
as part of this session though.

<a name="what"></a>
## What is Redux?
Redux is a tool you can use to manage your application state. The state will be
unique to the client that is interacting with application. Each client will have
their own version of the state.

> This state can include server responses and cached data, as well as locally
created data that has not yet been persisted to the server.

The state might also..

> need to manage active routes, selected tabs, spinners, pagination controls,
and so on.

Things get complicated when data is coming back in an asynchronous way so..

> Redux attempts to make state mutations predictable by imposing certain
restrictions on how and when updates can happen. These restrictions are
reflected in the three principles of Redux.

<a name="principles"></a>
## Three principles of Redux
The 3 core principles of Redux are:
1. **Single source of truth** - There is only one state object for the whole
application.
1. **State is read-only** - The only way to change it is by triggering an
action.
1. **Changes are made with pure functions** - Pure functions are deterministic.
This means, that given the same input(s), the function will always return the
same output.

Full details fo the three principles is available
[here](https://redux.js.org/introduction/threeprinciples).

<a name="when"></a>
## When do you need Redux?
Personally I'd use it in just about any React application I build, but it comes
into its own for medium or large applications which:
* work with data from multiple sources
* have complex UIs that can change dependent on user interaction

Redux provides a scalable approach to how you structure all your application
state which makes it much easier to test, debug and extend your code.

<a name="how"></a>
## How does Redux work?
Redux encourages you to break things down into a Store, Reducers, Actions and
Containers. These then interact with the views and components you've created in
React.

Here's a diagram that gives a bit of an overview of data-flow in Redux:

<img
  src="http://www.michaelridland.com/wp-content/uploads/2015/11/flux-diagram.png"
  alt="Redux Data-flow"
  width="70%"
  height="70%"
/>

### Store
At the heart of Redux there is the application **store** which is where all of
the application data being managed through Redux is held.

We can access data from the store, but it is read-only.

### Actions
The only way to modify the **store** is by using an **action**. Actions make no
assumptions about the current state of the data, they just provide information
about what they want the new data to be.

Here are some examples of actions from the Redux website:

* This action might add a new todo entry with the title 'Go to swimming pool':
  ```
  { type: 'ADD_TODO', text: 'Go to swimming pool' }
  ```

* This action might set the 2nd todo entry (indexes start at 0) to _done_ or
  _open_ depending on the todo entries current state:
  ```
  { type: 'TOGGLE_TODO', index: 1 }
  ```

* This action might remove a filter on the page and show all entries:
  ```
  { type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }
  ```  

Actions are plain JavaScript objects with a key called `type` which uniquely
identifies the action and they can optionally provide some additional associated
data using any other keys too.

### Reducers
Reducers listen for actions and contain the logic of how to process the action
in order to update the store.

You can have multiple reducers in your application that work with different
parts of the application store. One reducer might deal with user settings whilst
another might contain a todo list.

They make updates to the store using pure functions.

### Containers
Containers are referred to as controller-views in the diagram above but they're
usually known as containers.

They wrap around a component and give the component a way to read from the store
and to dispatch actions to update the store (for example on a click event).

They listen for changes to the store and then provide the new updates to the
view or component that they are associated with.

<a name="further"></a>
## Further reading
Redux was created by Dan Abramov and he has recorded some
[fantastic video tutorials](https://egghead.io/courses/getting-started-with-redux)
that take you through the whole process step by step. They're free but you do
need to set up an account to keep watching them. I can't recommend these
highly enough!

The [Redux website](https://redux.js.org/) also has lots of resources and is a
great starting point.  

You can use Redux with multiple frameworks.
[This part of the Redux docs](https://redux.js.org/basics/usagewithreact) will
tell you how to use it with React.  

There's a great [entry level example](https://redux.js.org/basics/exampletodolist)
of how to build a ToDo list with Redux.   

And also a [more advanced one](https://redux.js.org/advanced/exampleredditapi)
that uses asynchronous calls to the Reddit API.  
