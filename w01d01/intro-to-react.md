
Title: Intro to React<br>
Duration: 1hr+ <br>
Creator:  Joe Keohan<br>

---


# Intro to React.js

<img src="https://i.imgur.com/yt8BVNj.png" width=500/>

## Learning Objectives

* Explain what a frontend framework is and why it is needed for writing more complex applications.
* Explain what React.js is and where it fits in our applications' stack.
* Explain the component model of web development.
* Create and render React components in the browser.

## Framing

### The Rise and Fall of jQuery

Any Front End developer, with several years of experience in the industry, will have either heard of jQuery or worked with it directly. 

jQuery was first introduced in 2006 and just shy of [20 million web sites](https://www.similartech.com/compare/jquery-vs-react-js) have been built using the library vs. the 1 million+ for React.

<img src="https://i.imgur.com/ZquZoFk.png" /><br>

The jQuery `library` was the front end developers tool of choice for quite sometime but it's starting to run it's course. 

More and more developers are opting to use front end libraries that might also be considered  `frameworks` such as React, Vue and Svelt to name a few. 


### The Birth of the Frontend Frameworks

As the world of front end development and software engineering grows in complexity so does the need to create new tools that do the following:

- facilitate the development process across teams and industries
- develop a reusable code base comprised of **components**
- maintain the performance of the application across a diverse set of devices and browsers. 

Several years after the birth of jQuery several front end frameworks were introduced that provided a much more structured and opinionated way of writing code.  

Here are a few of the most well known frameworks and when they were introduced.

| Framework | Year Introduced |
| :---: | :---: | 
| Angular | 2009 |
| Backbone | 2010|
| Ember | 2011 |
| React | 2013 |


<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

- Think about what a front end framework is and answer the following questions:
  - How is it different than a JavaScript library like jQuery, Lodash, Underscore or Ramda? 
  - Why would we opt to use it?
- Write our you're answer in a slack thread to you'reself
- When asked slack you're answer in the thread created by the instructor

<hr> -->


<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 7min

The following questions are based on the article you were asked to read for homework: [javascript-frameworks-vs-libraries](https://skillcrush.com/blog/javascript-frameworks-vs-libraries/) 


Students will be placed in breakout rooms to discuss what a front end framework is and answer the following questions:
  - How is React different than a JavaScript library like jQuery? 
  - What benefit comes from using a framework like React?
  - When would you consider using a library and framework together? 
  
  The group will decide on a single cohesive answer to that question and pick a member to post their answer. 

:thumbsup: Click on the thumbs up when you're done.

When asked slack you're answer in the thread created by the instructor

<hr> -->

### Front End Frameworks

A framework is a library that provides generic functionality and structure and serves as the foundation to build and deploy applications.  

The following are just a few of the most popular front end frameworks mentioned in [https://2020.stateofjs.com](https://2020.stateofjs.com/en-US/technologies/front-end-frameworks/)

- React
- Angular
- Vue
- Svelte


### Sites Built On React

First, let's review a few of the most popular web sites built in React:

*   Facebook - They actually built React! 
*   Instagram - It's public feed and internal system are entirely built on React.


As you can imagine they are not the only popular sites built in React.  


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at this article  [The Best Websites Examples Built With React JS](https://www.monocubed.com/websites-built-with-react/).

Look over the sites and determine which ones you have used in the past or perhaps use on a daily/weekly basis.

When asked slack you're answer in the thread created by the instructor.

<hr>

<!-- ### The History of React

As mentioned before Facebook actually created React to meet the demands of the most popular social media platform of it's day. 

*   First used by Facebook in 2011.
*   Adopted by Instagram in 2012.
*   Made open source in May 2013.
*   Not long after React was embraced by the dev community. 

React was born out of Facebook's frustration with the traditional MVC model and:

  * how re-rendering something meant re-rendering **everything** (or just a lot).
  * how it had negative implications on processing power and ultimately user experience, which at times became glitchy and laggy. -->

### What Is React.js

React is a JavaScript `library` used to craft modern day UI for the front-end in web applications. It essentially takes the UI and breaks it down into reusable `Components`.  

By modeling small reusable `Components` that focus on just rendering a specific portion of the view,  React can improve an app's performance, maintainability, modularity and readability.

Components are such an integral part of React that many companies create Component Libraries, such as Shopify which created [Polaris](https://polaris.shopify.com/)

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - React Developer Tools - 5min

<!-- Let's take a look at a simple app built in React: <a href="https://02nz9.csb.app/" target="_">Mars Rebuild</a> -->

Let's take a look at a simple app built in React: <a href="https://nt8se.csb.app" target="_">StreetBall Mecca</a>

Looking at the sites UI we can't really see React.  It's there working under the hook but just not so apparent on the surface.  So let's peel back a layer and see React in action.  

This involves installing <a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en" target="_">React Chrome Developer Tools</a>

Take a moment to install the tool and then open `DevTools` to confirm the **Components** and **Profile** tabs have been added:

<img src="https://i.imgur.com/KsccFOw.png">

:thumbsup: Click on the thumbs up when you're done.

<hr>

<!-- ### React Alone Can't Build A App

React can co-exist with other Javascript libraries and frameworks.  If fact there are many helper libraries that developers use quite often like, `Lodash`, `Underscore` or `Ramda` which are great for performing adv JS functionality.  

 -->

### React in MVC

React is only used for the `front end` when buidling an app and would require working with other frameworks to handle 
the `models - (data)` and `controllers - (business logic)` while having React single handedly manage the `view`.

The MVC architecture is a JavaScript design pattern for building an applications. It isn't the only design pattern being used and others exist such as `MV*`, `MVP`, `MVVM` but the `MVC architecture` is used quite often and represents the following:

- `M stands for Model`
- `V stands for Views` 
- `C stands for Controller.` 

 The `View` is the presentation layer, it’s what the user sees and interacts with in the browser. The `Controller` makes the decisions based on requests and then controls what happens in response, like clicking on links and submitting forms and communicates with the `Model`, which is the database and returns data. 

 `React` is the `View` in this model. 

<img src="https://i.imgur.com/t779Jw9.png" width=600/>

The backed is represented here by `Controller` and `Model` and can be implemented using any backend framework such as:

- Node/Express 
- Ruby on Rails / Python & Django 
- PHP


Here is a <a href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/#detailmvcmvp" target="_">good reference</a> on the types of MV* patterns.



 ## The Virtual DOM For Efficiency

The `Document Object Model` or DOM for short is an API that is used to interact with the HTML that is displayed on a page.  The following structure represents the DOM and starts with the `document` object. 

<img src="https://i.imgur.com/qB0cznr.png" width=500/>

If you have ever used `document.getElementById('someid')` or jQuery's `$('#someid')` then you have worked with DOM. 


The **Virtual DOM** is a representation of the **actual DOM** and is a staging area for changes that will eventually be implemented. Because of that, React can keep track of changes in the actual DOM by comparing different instances of the Virtual DOM.

  <img src="https://i.imgur.com/xTxgF0b.png" width=500/>

React then isolates the changes between old and new instances of the Virtual
  DOM and then only updates the actual DOM with the necessary changes as opposed to re-rendering an entire
  view altogether which makes React significantly more efficient.


  <img src="https://i.imgur.com/RmHCcDu.png" width=500/>

  Here is a <a href="https://dev.to/maulik/the-best-example-to-understand-virtual-dom-4lfn" target="_">good example</a> that conveys the benefits of using React and it's Virtual DOM.


### Getting Started With React

So now it's time to get started with React. For this demo we will be using an online platform called  `CodeSandbox`. 

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min


- Go to [https://codesandbox.io](https://codesandbox.io) and sign  up for a free account
- :thumbsup: Click on the thumbs up when you're done.

<hr> -->

<!-- Here is the starter code we will be working with: <a href="https://codesandbox.io/s/getting-started-0q2sk" target="_">React CodeSandbox Starter</a> -->

Here is the starter code we will be working with: <a href="https://codesandbox.io/s/getting-started-forked-kq03v" target="_">React CodeSandbox Starter</a>

**Note:** Be sure to fork button on the top right:

<img src="https://i.imgur.com/KQSFfqE.png" width=300/>

<!-- **NOTE:** In order to easily share code, submit homeowrk and work through errors we will be using `CodeSandbox` for this remote course. -->

#### Configuring Our React App
A few things have been removed from this CodeSandbox so that we can focus on:

- Installing the required dependencies (libraries): `(react & reactDOM)`
- Importing the libraries into `index.js`
- Using `ReactDOM.render()` to render our initial content. 

#### Adding Dependencies

Let's add the dependencies first.  On the left side click on `Add dependency` 

<img src="https://i.imgur.com/Q9aLHqN.png" width=300/>

And then search for and add the following:

- `react` - used to create Components
- `react-dom` - used to manage the Virtual DOM
- `react-scripts` - used to transpile the code

Once they have been added it should look like the following.  Take note of the react version as React has gone through several iterations`.  

As of `16.8` React introduced `Hooks` which allowed **Functional Components** to **hook** into functionality previously available in **Class Components**. 

**Hooks** are the way to write modern day React and will use them throughout this class.  

<img src="https://i.imgur.com/VcARsI5.png" width=300/>

#### Setting Up index.js

In the left pane we should see the following.  This is essentially the default folder structure for the React App.

Both the `public` and `src` folders are very important in a React app. The `public` folder is what is sent to the end user and the `src` folder is used to write all our React code. 

<img src="https://i.imgur.com/pHKE3l4.png" width=300/><br>

The one element inside the `public/index.html` file that we need to be aware of right now is:

```html
<div id="root"></div>
```

This will be the element that React mounts to and uses to render the entire app. 

#### Importing The Libraries
Before you can work with React, or any library for that matter, we must import them into the file in which they will be used.  In our case let's import the libraries into `index.js`.

```js
import { createRoot } from "react-dom/client";
```

#### ReactDOM.render()
With our library in place we can use `createRoot()` to render either, a `Component` or plain `HTML` to the screen.  

Before we can render anything we need to tell React what element to use as it's mounting point which, in most cases is an element with and id of root.
```js
const rootElement = document.getElementById("root");
const root = createRoot(rootElement);
```

And now we can render some HTML.

```js
root.render(
  'Hello world'
);
```

We should see our app update to display the following:

<img src="https://i.imgur.com/sY8NkIg.png" width=300/>

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min


Let's take a moment to examine `public/index.html`


- Look for the element with an `id=root`
- Does it have any HTML directly inside of it? 
- Investigate the same element in `Chrome Developer Tools` and we should see the following:

<img src="https://i.imgur.com/kxwtvbn.png" width=300/>

Now, in the HTML, cut the entire element with `<div className=App>` and paste it over the `<h1>` in `index.js`. 

```js
root.render(
  <div className="App">
    <h1>Hello CodeSandbox</h1>
    <h2>Start editing to see some magic happen!</h2>
  </div>
);

```

React will re-render and our page should display the content.   

Take special note that once the element is rendered that React renamed `className` to `class`.  This happened as the keyword `class` is a reserved word in JS ES6for creating ES6 Classes and so React requires that we define css classes as `className`. 

<img src='https://i.imgur.com/LViMzXN.png' width=500/>

<hr>


<!-- 
Here is the final <a href="https://codesandbox.io/s/seir-831-getting-starter-forked-jogq5?file=/src/index.js:188-372" target="_">CodeSandbox Solution</a>. -->

### Solution Code 

Here is the final <a href="https://codesandbox.io/s/getting-started-2-14-22-9is0i?file=/src/index.js" target="_">CodeSandbox Solution</a>.

### Bonus - Becoming A React Developer

Learning React requires that one have an understanding and working knowledge of basic front end technologies, such as: 

- HTML
- CSS
- JavaScript (ES6, ES7, ES8) 

It then opens the door to a whole new world of development tools that are used in the React ecosystem.  

The [React Developer Roadmap](https://hackernoon.com/the-2020-reactjs-developer-roadmap-8q143yan) does a good job of documenting the technologies and concepts that one will be exposed to when working in React.

<img src="https://i.imgur.com/hZOSZbb.png" width=900/>

### Resources

- For an intro to React, watch [this video](https://generalassembly.wistia.com/medias/lr8idjxtx8).
- [Essential JS Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)
