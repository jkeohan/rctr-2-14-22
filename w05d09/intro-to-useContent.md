<br>
Title: Intro To useContent<br>
Duration: 1 - 1.5hrs <br>
Creator:  Joe Keohan<br>

---

# Context

### Learning Objectives:

- Explain how we simply code using abstraction
- Understand what Providers and Consumers are and what they do
- Implement a shared context to avoid prop drilling


## Framing Context

A good analogy of Context vs Props is when we shop online.  Props is like buying a product from a retailer instead of the manufactures.  Doing so adds one more step and additional overhead/cost to the whole process.  However Context is like buying the product directly from the manufacturer.  

`useContext` is one of the `3 Basic Hooks` that included with [React v16.8](https://reactjs.org/blog/2019/02/06/react-v16.8.0.html).  It provides a global form of state that child components can consume directly. It makes use of the `Provider/Consumer` model. 

<img src="https://i.imgur.com/yomTakB.png" />

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a few minutes to review the [useContext](https://reactjs.org/docs/hooks-reference.html)  hook official documentation

**Note:** As mentioned when used with `useReducer` the two Hooks create a low level version of [Redux](https://redux.js.org/), which is a state management tool for JavaScript applications and has become synonymous with React state management. 

<hr>

#### Where Does State Go?

As we've covered before, React has a unidirectional data flow, passing props from parents to children. Components that manage their own state will often pass this information down as props child components.

As our app grows, the `tree of components` grows with it. Soon the decision to create additional state may require that you pass pass and/or lift state further and farther in the React hierarchy.

<!-- How would you answer the following question: -->

<!-- <hr>

:question: **Where should you store and manage single or multiple instances of state in any of the apps you build?**

<hr> -->

#### Colocation
Where should state live? There are a lot of ways to answer this question but the best approach is to place state in the Component that need to make use of it,  which is also known as **Colocation**.  Kent C. Dodds put together a great article called [State Colocation Will Make Your React App Faster](https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster).

If we take a look at our [Shopping Cart](https://codesandbox.io/s/react-shopping-cart-input-solution-cmix9?file=/src/App.js) assignment we can see that it makes more sense to place state in both the App and Form Components.

 <img src="https://i.imgur.com/SdWgQNt.png" />

<!-- <details><summary>Answer</summary>

**Manage state in the Component or nearest "ancestor" of the components that need to make use of it**.
 
 <img src="https://i.imgur.com/SdWgQNt.png" />

</details> -->


### App-level state

We discussed this briefly when we covered *lifting state* - where we had two sibling components that needed to share some state so we "lifted" the state up to the parent component.

But, there are times where pieces of state need to be used across the entire app. For instance:

 - When many views & UI components need to know who the currently logged-in user is.
 - When all UI components need to know if the app is in "light" or "dark" mode.


### Avoiding Prop Drilling

So far, we have been passing down down from parent to child components. In most instances, this is the easiest way to pass information between parent and child components.

But, as your tree grows, you'll find yourself passing props down multiple levels. In the example below sending a single value of state all the way down to the the last child requires passing it down as props through every intermediary Component in the hierarchy. 

<img src="https://i.imgur.com/G08K3c9.png" width=400/>

#### The useContent Hook

A much better way would be to provide access to state at a global level and have the child Component access it directly.  This is where we would create a global context which the **useContext** hook would consume. 

<img src="https://i.imgur.com/izs3Rxn.png" width=400/>

### Summary: When & Why to use Context

So the two main reasons we should make use of useContext are: 

- Avoiding Prop Drilling
- Provide access to App-level state to components dispersed through the app hierarchy

## Context Provider and Consumer Model

When making use of Context, you'll be dealing with **Provider** and **Consumer** components.

**Providers** are components that exist higher up on the tree, sending - or _providing_ - state to other components further down the hierarchy. 

**Consumers** are components that receive - or _consume_ - state from their Provider. Consumer components 'extract' the desired state values to be used them in our own components.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Lets take a look at [AirBnB](https://www.airbnb.com/) in DevTools in order to see the `Provider/Consumer` model in action. 

And let's also take a look at how a [Theme](https://lt9tx.csb.app/) can be passed using the **useContext**.

<hr>

### React Router Provider > Consumer Example 

Another example of the Provider > Consumer model is `React Router`.  If you haven't already worked on the [iStocks App](https://vhixt.csb.app/) React router assignment then it's something we will get to in the next few lessons.  

For now just know that `React Router` uses the `Provider > Consumer` model which is visible in React DevTools.

<img src="https://i.imgur.com/Muw1Jxm.png" width="400">

Also another thing to note is that `React Router` creates and passes the following props using the `Provider > Consumer` model.

```js
this is Home - props 
{history: {…}, location: {…}, match: {…}, staticContext: undefined}
history: {length: 1, action: "POP", location: {…}, createHref: ƒ, push: ƒ, …}
location: {pathname: "/", search: "", hash: "", state: undefined}
match: {path: "/", url: "/", isExact: true, params: {…}}
```

---

## Instructor Demo Of Prop Drilling

The Instructor will perform a demo of using `prop drilling` to pass state from App to it's lowest level child Components.  

In this demo we will be using the following starter code: [React Context CodeSandbox](https://codesandbox.io/s/usecontext-starter-dont-edit-4v65w?file=/src/components/App.js)

<!-- Here is the [Prop Drilling Solution Code](https://codesandbox.io/s/usecontext-solution-prop-drilling-wvfrc?file=/src/components/ComponentD.js) -->


## Working With React Context

<!-- In this demo we will be using the following starter code: [React Context CodeSandbox](https://codesandbox.io/s/usecontext-starter-dont-edit-4v65w?file=/src/components/App.js) -->

Working with React Context involves setting up context in the parent Component and then consuming it in the child.  In order to work with context  we will need to do the following:

In the **App Component**:
- import `createContext` from react
- create and export an instance of `createContext`
- set up a `context.Provider `
- provide the data via the `context.Provider`

In the **Child Components**:
- import the `useContext`
- import the `context` from App
- instantiate `useContext` to use the imported `context` from App


## App Component

### Importing and Using `createContext`

Before we can work with context we first need to import `createContext` from React. 

```js
import React, { createContext } from "react";
```

Now we instantiate and export a new instance `createContext`. 

```js
export const DataContext = createContext()
console.log('DataContent', DataContext)
```

This function returns an object with two properties, `Provider` and `Consumer`:

<img src="https://i.imgur.com/PessZNU.png" />

### Setting Up The Context Provider

The `Provider` is wrapped around the Components that we wish to provide the context.  It requires a single prop called `value` which is assigned the data we wish the child Components to consume. 

In this example we will pass the userData that has been imported and stored in state. 

```html
<DataContext.Provider value={userData}>
    <ComponentA />
    <ComponentE />
</DataContext.Provider>
```

## Child Components
The child Components will now consume the data.  Consumers must first import `useContext` and the Context provided from the parent Component.

```js
import React, { useContext } from "react";

import { DataContext } from './App'
```

**useContext**

Let's now setup `useContext` to use the context imported from App. 

```js
const dataContext = useContext(DataContext)
```

And now we can access that data.

```js
function ComponentD() {
  return (
    <div style={style}>
      This is Component D
      <div> 
        <div>username: {dataContext.name}</div>
            <img
            class="avatar-image"
            src={dataContext.img}
            alt="avatar"
          />
      </div>
    </div>
  );
}
```

Here is the [final solution code](https://codesandbox.io/s/usecontext-demo-solution-tujgu?file=/src/components/App.js) 


# Resources
- [React v16.8](https://reactjs.org/blog/2019/02/06/react-v16.8.0.html)
- [useContext](https://reactjs.org/docs/hooks-reference.html) 
- [Light and Dark theme using context example](https://reactjs.org/docs/context.html#dynamic-context)
- [Create a low level version of Redux](https://www.robinwieruch.de/redux-with-react-hooks)
- [Redux](https://redux.js.org/)
