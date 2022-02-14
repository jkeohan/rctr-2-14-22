<br>
Title: Nested Components<br>
Duration: 1hr+ <br>
Creator:  Joe Keohan<br>

---

# Nested Components

## Learning Objectives

*   Break down an HTML layout into multiple Components
*   Create reusable Components to be used in other design layouts
*   Nest Components to implement the current design

## Components

As we've explained `Components` are the fundamental building blocks of React and let you split the UI into independent, reusable pieces, and be able to use each one in isolation.  

This is very similar to the way we write JavaScript functions.  They are meant to be `independent` and `reusable`.  By passing in `standardized` input they will return `standardized` output.  

 Components behave under the same premise and, if configured to accept input, will return UI that is either includes the input or has influenced how the input is displayed. 
 
 The input we pass to a Component is called a `prop` and we will use them extensively in any React app we build.  

### Nested Components

Let's revisit the Bootstrap card example.  It provides all the HTML needed to produce a standard `card` and, along with Bootstrap css, styles the card quite nicely. 

Here is the HTML provided by Bootstrap:

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

In order to bridge the gap of what defines a Component, we will be creating a custom React `Card` Component that uses the Bootstrap HTML. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Open and fork the following <a href="https://codesandbox.io/s/components-bootstrap-starter-o2ry1?file=/src/App.js" target="_">CodeSandbox Card Starter</a>

:thumbsup: Click on the thumbs up when you've forked.

<!-- https://codesandbox.io/s/seir-831-bootstrap-starter-sv30w?file=/src/index.js -->

You should see the following:

<img src="https://i.imgur.com/NaGIt48.jpg" width=400/>

- Take a moment to examine the code.  
- See if you can determine where the `H1` is being rendered
- See if you can determine where the 2 cards are being rendered

:thumbsup: - Click on the thumbs up when you're done.

- Slack you're answer in the thread created by the instructor

<hr>

Our investigation should have determined the following:

- `App` Component - renders the H1
- `public/index.html` - renders the cards

**Note:** You might have noticed that the App Component was written slightly differently then before.  It's being both created and exported at the same time. 

```js
export default function App() {
  //...rest of code
}
```

For the time being we are going to write the Component and export it separately as we want to make our code more readable.

#### Creating A Component

So let's take a moment to create a `Functional Component` that contains all the Bootstrap HTML code needed to allow us to create the 2 card Components as per our layout.  

In the `src` folder create the following files:

- Card1.js
- Card2.js

:thumbsup: Click on the thumbs up when you're done.

**Card1**

Let's begin with the `Card1` Component.  

Inside of `Card1.js` let's do the following for now:

- Import React
- Create the Component
- Export the Component

```js
// IMPORT REACT
import React from 'react'

// CREATE THE COMPONENT
const Card1 = () => {
  return (
    <div>Card1</div>
  )
}

// EXPORT THE COMPONENT
export default Card1
```

:thumbsup: Click on the thumbs up when you're done.

#### Nesting A Component

As with any layout design, HTML elements must be nested inside other elements to achieve the desired effect.  

This is no different for React and since our goal is to render an `H1`, as well as the `cards`, we must call the `Card1` Component within the `return` statement of it's parent Component, in this case `App`. 


```js
// IMPORT CARD1
import Card1 from './Card1'

export default function App() {
  return (
    <div className="App">
      <h1>Bootstrap Cards To Component Example</h1>
      <Card1 />
    </div>
  );
}
```

If successful you should see the following:

<img src="https://i.imgur.com/jHnPLLv.png" width=200/><br>

:thumbsup: Click on the thumbs up when you're done.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

**NOTE:** Before you perform the steps we ask that you do not copy/paste at this time and write everything from scratch.  

In time copy/paste will be the most efficient way to create Components, however you are just learning how to write Components so the additional manual work will help solidify these concepts.

- Perform the same steps as you did for Card1
- Only change it's HTML output to be `Card2`
- Make sure to render Card2

you're code should produce the following:

<img src="https://i.imgur.com/MOiPdAA.png" width=200/><br>

:thumbsup: Click on the thumbs up when you're done.

<hr>

Now it's time to output the HTML that represents each Component.  This, as we we discovered earlier, is found in `public/index.html`

Cut the entire `<div class='card>...</div>` for the first card and place it inside of `Card1`

```js
const Card1 = () => {
  return (
    <div class="card" style="width: 18rem;">
      <img
        src="https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60"
        class="card-img-top"
        alt="..."
      />
      <div class="card-body">
       <h5 class="card-title">Card 1</h5>
        <p class="card-text">
         Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </div>
  )
}

```

:thumbsup: Click on the thumbs up when you're done.

We should be immediately encounter the following error:

<img src="https://i.imgur.com/u9Uvwg9.png" />

This has to do with a rule related to JSX which is:

:oncoming_police_car: Any JS within JSX must be enclosed in curly braces `{}`

Since style accepts an object with the css key:value pairs (first set of curlys) we then need to surround that in an additional set of curlys.  

So the `style` prop must be written in the following format:

```js
style={{key: value}}
```

Let's update our Component to include the proper syntax

```js
<div class="card" style={{width:'18rem'}}>
```

The other JSX rule we must follow is:

:oncoming_police_car: - The keyword class is reserved so classes must be renamed `className`

So we need to rename every instance of `class` to `className`.  

:thumbsup: Click on the thumbs up when you're done.

Here is our Component with those changes:

```js
const Card1 = () => {
  return (
    <div className="card" style={{width:'18rem'}}>
    <img
      src="https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60"
      className="card-img-top"
      alt="..."
    />
    <div className="card-body">
      <h5 className="card-title">Card title</h5>
      <p className="card-text">
        Some quick example text to build on the card title and make up the
        bulk of the card's content.
      </p>
      <a href="#" className="btn btn-primary">Go somewhere</a>
    </div>
  </div>
  )
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

- Perform the same steps to Card2 as you did for Card1 
- Make sure to render Card2
- Refresh the page to see the changes

you're code should produce the following:

<img src="https://i.imgur.com/MOiPdAA.png" width=150/>

:thumbsup: Click on the thumbs up when you're done.

<hr>

In the original design the cards were sitting next to each other.  

The reason they are no longer doing so is because we did not include the parent `<section class="cards">` element.  

Let's add that to the App Component.

```js
export default function App() {
  return (
    <div className="App">
      <h1>Bootstrap Cards To Component Example</h1>
      <section className="cards">
        <Card1 />
        <Card2 />
      </section>
    </div>
  );
}
```

If everything worked we should now see our original design in place.

<img src="https://i.imgur.com/nsN0Cro.jpg" width=400/>

### More Nested Components

When we look at both cards displayed on the page I feel the need to ask myself are there any sections of the card that could be used in another design layout.  

Say you if removed the image and were left with just the `title`, `text` and `button`.  Would another layout design benefit from just that grouping of elements? 

Or perhaps the image could be a reused as well as it's own independent element. And why not the button. 

If we took just a moment to actually visualize these Components it might look something like this: 

<img src="https://i.imgur.com/LaD44H7.pngv" width=500/ >

So it seems there is an opportunity to create and reuse additional components.  

So let's spin off a few more Components and then import them into the Card Components.

#### Card Body Component

Let's start with creating a separate `CardBody` Component and have it render the card body html.  

In order to that we must perform the following steps: 

- Creating a new CardBody.js file
- Importing React
- Creating the Component
- Copying the HTML for the card body
- Exporting the Component

```js
// IMPORT REACT
import React from 'react'

// CREATE THE COMPONENT
const CardBody = () => {
  return (
     <div className="card-body">
      <h5 className="card-title">Card title</h5>
      <p className="card-text">
        Some quick example text to build on the card title and make up the
        bulk of the card's content.
      </p>
      <a href="#" className="btn btn-primary">Go somewhere</a>
    </div>
  )
}

// EXPORT THE COMPONENT
export default CardBody
```

:thumbsup: Click on the thumbs up when you're done.

#### Render The CardBody Component

We now have a separate Component altogether which we need to import and render into the Card Component. 

In Card1.js do the following:

- Import the CardBody Component
- Replace the card-body element with `<CardBody />` Component

```js
import CardBody from './CardBody'

const Card1 = () => {
   return (
    <div className="card" style={{width:'18rem'}}>
      <img
      src="https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60"
      className="card-img-top"
      alt="..."
    />
      <CardBody />
  </div>
  )
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min

If we follow the basic pattern we can create and render new Components relatively easily. 

Now it's you're turn to do the following:

- Create a CardImage Component that returns the just image
- Create a Button Component that returns just the button
- Import CardImage into Card1
- Import the CardButton into CardBody
- Replace the HTML with those Components

:thumbsup: Click on the thumbs up when you're done.

<hr>

<a href="https://codesandbox.io/s/seir-831-bootstrap-solution-r8p9i?file=/src/CardBody.js" target="_">Solution Code</a>

### Lab Time

The instructor will provide the lab.
