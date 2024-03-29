<br>
Title: Lifting State<br>
Duration: 1hr + <br>
Creator:  Joe Keohan<br>

---

# Lifting State

## Learning Objectives

After this lesson you will be able to:

- Learn to design a React architecture 
- Place state closest to where it needs to live
- Pass functions down to child Components as props
- Lift data from child to parent Component


## Framing

### The Chain of Command
The chain of command is one of the foundational elements of any successful organization.  Decisions are made at the the very top and then passed down the change of command to execute.  Each group along the way has certain freedoms to carry out the tasks at hand as long as they adhere to the rules and policies that are in place. 

Some decisions will be executed at specific levels while others need to first be run past a  manager for approval. This need to elevate a request up the chain is an example of `lifting state`.  

Once a decision is made it is then passed back down the chain of command to all those involved with making the request. 

## React State
React state works in a similar fashion. Props are passed down to child Components and, if needed, data can be lifted back up to the parent Component is a process called `lifting state`.

Lifting state will almost always cause the parent element to update it's own state thereby triggering a re-render which then allows the parent to passing some mutated version of the data back down as props. 

It's also important to note that state should be placed nearest to the Component that needs it.

<!-- ### Rules Of State
:oncoming_police_car: - Rules (Component Specific)

- Data in React is unidirectional and props are always passed down from parent > child
- Child Components cannot communicate directly and therefore cannot pass data between them
- Child Components cannot pass data directly to each other and must lift data to parent which then passes it back down as props
- Functions passed as props are how state is lifted -->


### Component Hierarchy 

So far we've learned how to create nested Components, pass props and set/update state.  The goal has been to get you comfortable with all of the smaller moving parts before we attempt to put them all together and create much larger applications. 

Now it's time to take it one step further and start thinking about the entire React hierarchy as a whole. 

Building out an app involves asking questions like the following:

- What components are needed?
- How should they be organized? 
- What props need to be passed down?
- What state needs to be lifted?
- Where should state reside and what should that state look like? 

The answer to these questions is key to the success of your application and, as there are many options to think through, there is much planning needed to design an intuitive and efficient architecture. 

### Lifting State In React Cities

Let's take a look at `Cities Of The World`.  The app is divided into small images, each of which represents a city.  

Clicking on any small image will assign the big image the same image url. 

Here is a [working CodeSandbox](https://iqcwj3.csb.app/) of the app.

<!-- Here is a [working CodeSandbox](https://codesandbox.io/s/rctr-react-cities-base-solution-iqcwj3) of the app which we will use as our starter code.
 -->

 <!-- Here is our [Starter CodeSandbox](https://codesandbox.io/s/rctr-react-cities-base-solution-2-14-22-v7bjt0?file=/src/App.js) of the app which we will use as our starter code.
 -->

<img src="https://i.imgur.com/LI6KqAI.jpg" width=300/><br>

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 7min

Let's take a minute to update the starter code to add state in order to reproduce the same functionality. 

Here is our [Starter CodeSandbox](https://codesandbox.io/s/rctr-react-cities-base-solution-2-14-22-v7bjt0?file=/src/App.js) of the app which we will use as our starter code.

<hr>

### Refactor
 
It consists of a single `App` Component and one instance of `state` which keeps track of the last image clicked.  Since all functionality lives in one Component there is currently no need to `lift state`.  

In order to `lift state` we need to add some additional Components. For this design it seems the following Components would work for our design:

- BigImage
- SmallImage

#### Current React Hierarchy
This is the React Hierarchy of the app.  It consists of a single Component that contains state and renders all the HTML needed for the app.  

<img src="https://i.imgur.com/flWudXR.png" width=300/>

Although the design works just fine as is, we've decided to create additional Components to further segment the app.  

#### Redesigned Hierarchy
Based on our design decision this is the React Hierarchy we are looking to implement.  The diagram also includes a legend to indicate which Components contain state and which do not. 

<img src="https://i.imgur.com/WkLBY2i.png" width=400/>


As we can see App is still responsible for looping over the initial array and creating multiple instances of small images but now those images will be rendered via the `SmallImage` Component.

We can improve the drawing a bit to include what props will be passed down to the children. 

<img src="https://i.imgur.com/QyabBqU.png" width=600/>

What might stand out is the props highlighted in green called `handleClick`.  This is the same `handleCLick` function used in App but now it's being passed down to the child.  

When that function is called in the child Component it will be passed a value which is `lifted` back  to the parent.  That value is then used to update the `bigImage` state value, triggering a re-render and the new value for bigImage is passed back down to the `BigImage` Component. 

<img src="https://i.imgur.com/vwlWb2Z.png" width=600/>

Now it's time to do a little refactoring in order to implement the new hierarchy design. 

#### BigImage Component

Let's start with creating the BigImage Component.  Here are the steps we need to perform:

- Create a new file for the Component
- Create the Component
- Return some form of JSX 
- Exporting the Component
- Import the Component into its parent Component. 

**Setup The Components**

Create the file and setup the Component. This involves adding a parameter called props, copy/paste the existing HTML from App and then referencing the `props.image` key which will contain the image url. 

We could also make additional decisions such as passing down specific values for `id` and `alt` as to make this Component more reuseable, but we will leave those values alone for now and stay focused on the main value for the image src. 

`BigImage.js`
```js
import React from 'react';

const BigImage = (props) => {
 return (
  <img src={props.image} id="bigimage" alt={props.city}/>
 )
}

export default BigImage
```

`App.js`

App now needs to import and render the `BigImage` Component.

```js
import React, {useState} from 'react';
import './styles.css';
import imagesArr from './imageData'
// IMPORT CHILD COMPONENTS
import BigImage from './BigImage'
```

Let's replace the HTML with the `<BigImage />` Component and also make sure to pass it a prop. 

In this case it will be: `<BigImage image={bigImage} />`

```js
return (
    <div className="App">
        <h1>Cities Of The World</h1>
        <div id="wrapper">
            <div id="thumbnails">
            {images}
            </div>
            <BigImage image={bigImage} />
            {/* <img src={bigImage} id="bigimage" alt='bigImaage'/> */}
        </div>
    </div>
)
```

If we test the app now it should still work as before.  

Also take a minute to investigate the Component in `React Dev Tools`.


`SmallImage.js`

This will follow the same steps but will require a bit more refactoring as it is being rendered via `Array.map()` and has been configured to use an `onClick` event which calls the `handleClick` function. 

First let's create the Component.

```js
const SmallImage = (props) => {
    return (
        
    )
}
```

Let's copy the `<img>` element from the map and paste it in the `SmallImage` Component

```js

const SmallImage = (props) => {
    return (
        <img
            className="thumb"
            id={image.city}
            src={image.img}
            alt={image.city}
            onClick={() => handleClick(image.img)}
        />
    )
}
```

The only prop that needs to be removed when we copy the HTML into this Component is `key={index}`.  

**NOTE**: The `key:value` pair is only required within the `Array.map()`. 

Since the values for `id, src, alt` will be passed down from the parent we will need to update them to replace `image` with `props`

```js
const SmallImage = (props) => {
    return (
        <img
            className="thumb"
            id={props.city}
            src={props.img}
            alt={props.city}
            onClick={() => handleClick(props.img)}
        />
    )
}
```

**Lifting State**

The last item to precede with props is `props.handleClick`.  The expectation is that the parent element will pass this function down which we will call in the child in order to `lift state`. 

```js
import React from 'react';

const SmallImage = (props) => {
  
    return (
        <img
            className="thumb"
            id={props.city}
            src={props.img}
            alt={props.city}
            // key={index} - this is no longer needed here as it is only assigned within the loop
            onClick={() => props.handleClick(props.img)}
        />
    )
}

export default SmallImage
```

`App.js`

Let's import and render the SmallImage Component


```js
import React, {useState} from 'react';
import './styles.css';
import imagesArr from './imageData'
// IMPORT CHILD COMPONENTS
import BigImage from './BigImage'
import SmallImage from './SmallImage'
```

And update the .map() to include the Component

```js
const images = imagesArr.map( (image, index) => {
    return (
        <SmallImage 
            id={image.city}
            src={image.img}
            alt={image.city}
            key={index}
            handleClick={handleClick}   
        />
    )
})
```

##### React Dev Tools

If we take a look at React Dev Tools we should see the following:

<img src="https://i.imgur.com/7316yEY.png" />

#### Bonus - Using Object Destructuring

As we might recall **Object Destructuring** allows us to create variables and assign them values by eliciting those same `key:value` pairs from an object

Let's make use of the for `SmallImage`.

```js
import React from 'react';

const SmallImage = ({city, src, handleClick}) => {
  
 return (
  <img
    className="thumb"
    id={city}
    src={src}
    alt={city}
    {/* key={index} - this is no longer needed here as it is only assigned within the loop */}
    onClick={() => handleClick(src)}
  />
 )
}

export default SmallImage
```

### Solution Code

[Solution CodeSandbox](https://codesandbox.io/s/cities-multiple-comp-lift-state-m9kt6?file=/src/App.js) 

<!-- ### Lab Time

The instructor will provide the lab -->
