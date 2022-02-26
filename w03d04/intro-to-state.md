

Title: Intro to State<br>
Duration: 1.5 - 2hrs <br>
Creator:  Joe Keohan<br>

---

# Intro to State

<img src="https://i.imgur.com/KRmlOo1.png" width=500/>

## Learning Objectives

After this lesson you will be able to:

- Explain what **state** is and how to implement it in a React Component
- Create **state** using the **useState** Hook
- Update **state** to trigger Component to re-render

## Framing

The best analogy to understand React **state** is to answer the following question: **How are you feeling this very moment?**

- Are you happy to be in class learning a new topic?
- Are you feeling tired after a long day at work?
- Did some random person say **hello** out of the blue and make you smile?

The answer to any of those questions has a direct impact on your **state** of mind.  A **happy** state will be reflected in your smile, tone of voice, and perhaps even being nice to others in return. An **unhappy** state will have the opposite effect.

As with all human beings our **state** of mind can change on the fly which is almost always reflected in our physical expressions or actions. Applications also have a **state** which is reflected in the UI presented to the user.

Therefore updating an applications **state** is our control mechanism for how we update the UI.

<!-- <img src="https://i.imgur.com/O0OwmJx.png" width=400px/> -->

## Props Recap

So far we've worked with **props** and used them to pass values down from a **parent** > **child** Component. This pattern of passing data down is consistent with React's unidirectional data flow pattern. 

We also know that the props passed down to a child are organized, by React, into an object where every prop becomes a **key:value** pair.

Props are a great way to pass data but have the following limitations:

- Props must be passed down from parent > child
- Reassigning a prop value will have no effect in the Component.
- Child Components cannot use props to pass data to their parent or other sibling Components

<hr>


#### :mag: - Check for Understanding 

Take a a minute to think about the following question:
  <!-- - What do we use **props** for?
  - What limitations do **props** have? -->
  - Is there any best practice you can think of when creating and passing a **prop**?

When asked slack your answer(s) in a thread created by the instructor

<!-- <details><summary>Best Answer</summary> -->


</details>
<hr>

## Intro To State

In our attempt to provide a coherent framing of React **state** the point was made that what you see on the page is the current version of the applications **state**. Any changes to **state** will then be reflected in the UI.

One important thing to note here is that any changes to state will cause the Component to **re-render**. This is essentially how the UI is updated. 

This is a very important concept to keep in mind as a **re-render** can also initiate additional function calls, something we will discuss as part of Reacts **lifecycle methods**.

### React Lifecycle

<img src="https://i.imgur.com/njO9Lfv.png">


<!-- ### Rules Of State
:oncoming_police_car: - Here are the rules we need to follow when working with state. 

- State is assigned using the **useState** hook
- The State value can be assigned any data type
- The State value is never updated directly but only using its corresponding **setState** function
- The current State value must always be overwritten with a new value  -->


### Working With State

So updating state will, most often, require the user to interact with the application. Hence, the user performs some action, like clicking a button, and the component responds by **doing a thing** which results in changing some values and then updating **state**. The steps are as follows:


### A Simple Counter Component

We'll walk through building a very simple **Counter** Component which will do the following:

-  provide the user 2 buttons to **increment** or **decrement**
- display the **initial** and **updated** value as it changes 

#### Spin Up A New CodeSandbox

For this demo you will spin up a new CodeSandbox. To do this just click on the blue **Create Sandbox** button on the right of the page. 

<img src="https://i.imgur.com/N0qsmdh.png" width=200/>

Now scroll down to the **Official Templates** section and choose **React by CodeSandbox**.

<img src="https://i.imgur.com/dgdr5A8.png" width=300/><br>

:thumbsup: Click on the thumbs up when your done.

#### Creating The Counter Component

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

Since you already have experience creating Components take a minute to perform the following activity.

**Counter Component**

- Create a new file in **src** called **Counter.js**
- Import React from 'react' 
- Create the **Counter** Component
- Return the following HTML:

```js
<>
    <span>Current Count: 0</span>
    <section>
        <button>+</button>
        <button>-</button>
    </section>
</>
```

- Export the Component

**App Component**

- Import the **Counter** Component into **App.js**
- Replace all the html inside of **className="App"** with the **Counter** Component.

```js
<div className='App'>
	<Counter />
</div>
```

Once your done React should render the following:

<img src="https://i.imgur.com/fBEOYU0.png" width=300/>

That HTML looks like it could use a little styling.  So lets copy/paste the following css to **styles.css**

<details>
<summary>CSS</summary>


```css
.App {
	font-family: sans-serif;
	text-align: center;
	width: 160px;
	margin: auto;
	display: flex;
	flex-direction: column;
}

section {
	display: flex;
}

button {
	flex: 1;
}

span {
	font-size: 20px;
}
```

</details>

<br>


And now the design should look like this:

<img src="https://i.imgur.com/jTh9SU2.png" width=200/>

<hr>

### The useState Hook

In order to add state to the **Counter** Component we will first need to import the **useState** Hook from **React**. **useState** is one of the 3 Basic Hooks as per the Official React Doc.

#### A Word On Hooks

Hooks were introduced in **React Version 16.8**. Before hooks, state was only available to a **Class** component. 

Hooks introduce state management to **Functional** components, using a simpler and more flexible API that let you split one component into smaller functions based on what functionality was needed.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Since we will be working with **Hooks** solely in this class let's take a minute to review the following React Docs:

- [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html) - all the available Hooks

<!-- **Class Compoonent State Example**

Class components come with a lot of boilerplate, which can feel bulky, especially when dealing with a simpler state. 

**Instructor Demo**

> The instructor will perform a small demo of creating a class based Component that includes state.  Not need to code along as none of the following code will be used in building the Counter App. 

Here is how state would have been configured using a class Component. 

```js
class Counter extends React.Component {
  constructor(props){
    super(props)
    this.state = {count: 0}
  }
  render() {}
}
```

However it is possible to shorten the above syntax to the following: 

```js
class Counter extends React.Component {

  state = {count: 0}

  render() {}
}
``` -->

<hr>


### Importing useState

Now it's time to import **useState** into the Counter Component. The **useState** function resides inside the **React** object so let's first peak inside. 

```js
import React from 'react';
console.log('this is React', React)
```

Here are a few of the Hooks available, including **useState**

<img src="https://i.imgur.com/soVHfMl.png" width=500/>

From the console log output it's clear to see that these **Hooks** are **key:value** pairs inside the **React** object. 

Since we were introduced to **Object Destructuring** let's use it to elicit the **useState** function and store in a variable.


```js
import React, { useState } from 'react';
```

Just so that we get a better idea of what **useState** actually is let's console log it as well. 

```js
const Counter = () => {
  console.log('useState - ', useState)
  // ...rest of code
}
```

The output should look like the following:

<img src="https://i.imgur.com/IZFNnbg.png" width=400/>
<br><br>

It appears that **useState** is a function that takes in **initialState** and returns **dispatcher.useState(initialState)**. 

We won't get into the underlying code here but one thing to highlight is the keyword **dispatcher**. 

We will revisit this concept later when we cover the **useReducer** hook as it uses a similar naming convention of **dispatch** for its **setState** function.

<hr>

#### useState Rules and Best Practices

Let's take a moment to once again review the **rules** of **useState** and cover some best practices as well. 

:oncoming_police_car: - Rules 

- the state value is never updated directly
- the state value is only updated using it's corresponding **setState** function
- the state value must always be overwritten with a new value 

:star: - Best Practices

- Use **Array Destructuring** when initializing the state variables
- Name the initial state based on what it contains
- Use the same name for the setState function but precede it with the word **set**
- Give thought as to what needs to be in state and how that state should be organized 
- Always use **...spread** operator to copy object and array values to the new state

<hr>

#### Creating An Instance Of State

With **useState** imported it's time to create an instance of state. To do this we will call **useState()** and pass it an initial starting value of **0**.

:star: - Name the initial state based on what it contains. 

```js
const countState = useState(0);
```

Once again let's add a console log and see what it returns.

```js
const countState = useState(0);
console.log('countState -', countState);
```

We should see the following:

<img src="https://i.imgur.com/0SIS9qZ.png" width=300/>

So it appears **countState** is set to an array that contains the following elements:

- 0 - the initial state value we defined
- a **function** - which will be used to update state.

<!-- One way to create 2 new variables based on the array would be to manually elicit their values using standard array bracket notation. 


In keeping with best practices we will name the initial state variable **count** as it will be used it to increment/decrement a starting value essentially keep **count**.

:star:  - Use the same name for the function but precede it with the word **set**

 Of course, the corresponding function that will be used to update state should be called **setCount**.

:star: - Use the same name for the function but precede it with **set**

```js
const count = countState[0];
const setCount = countState[1];
``` -->

#### Array Destructuring 


:star: - Use **Array Destructuring** when initializing the state variables: [Array Destructuring](https://javascript.info/destructuring-assignment). 

Array Destructuring elicits the values from the array based on their position  and stores them in variables. 


```js
const [count, setCount] = useState(0);
```

### Using State

Now that our initial value is been assigned to the **count** variable let's update the JSX to use that value instead of a current hard coded value of 0. 

Of course JSX requires that all JavaScript be surrounded in curly braces.


```js
return (
  <div>
    <span>Current Count: {count}</span>
    ... rest of code
  </div>
);
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

With our event handlers in place let's take a look at **React DevTools** 

If you highlight **Counter** it should look like the following:

<img src="https://i.imgur.com/hncbSl7.png" />

<hr>

### Updating State

With our state value in place it's time to provide some functionality to the buttons and allow the user a means to interact with the app and update state.

In the case of our Counter the only way to update  **count** is to call the **setCount** function and pass it a new value. 

:oncoming_police_car: - Always use the **setState** function to update state

There are 2 ways to perform this action:

```js
// grab the current version of state
setCount(count + 1);

// OR

// use a callback function and pass the previous version of state
setCount((prevState) => prevState + 1);
```
In the second example the **setter** function takes in a **callback function** that is passed the previous value of state and returns a new value altogether. 

The argument in this example is called **prevState** by convention but you can name it anything you want. 

There are scenarios when the callback function version is required, such as when state is being updated within the callbacks of either a **setTimeout()** or **setInterval()**.  Since that isn't the case here we will use the first example to update state. 


#### Adding an onClick Event

In order to allow the user to interact with the buttons we will need to add an event listener.

React provide **synthetic events** which correspond to underlying JS events.  

Events you might have worked with before are: 

- click => onClick
- submit => onSubmit
- change => onChange
- mouseover => onMouseOver


For now we will add an **onClick** event listener that calls **setCount** to update state.

Also, as with plain JavaScript or jQuery we will use an anonymous callback to pause the execution until the click event has occurred.

```js
  return (
    <div>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={() => setCount(count + 1)}>+</button>
        <button onClick={() => setCount(count - 1)}>-</button>
      </section>
    </div>
  )
```

If we test out the app we should see that the count value will change based on user input. 

<hr >

**Instructor Demo**

> The instructor will demo where React is caught in an infinite loop that was triggered by updating state without using the onClick callback function

<hr>

### Event Handlers

Working with React certainly requires that we write code in very opinionated ways which is why it's considered a **Framework**.  That is a good thing in that we can quickly examine code and expect some consistency in how it is written.

But some React code is written solely based on the adoption of the community at large.  One such pattern is the naming convention when creating **event handler** functions.  The convention is to precede their name with word **handle**.

Let's give that a try by creating the following supporting functions:

- **handleIncrement**
- **handleDecrement**

```js
const handleIncrement = () => {};

const handleDecrement = () => {};
```

Now let's move the **setState** function calls into their corresponding **handler** functions and update the **onClick** to reflect this refactor. 

```js
const handleIncrement = () => {
	setCount(count + 1);
};

const handleDecrement = () => {
	setCount(count - 1);
};

<section>
	<button onClick={handleIncrement}>+</button>
	<button onClick={handleDecrement}>-</button>
</section>;
```

The other added benefits of using these supporting **handler** functions are:

- its a much better way to organize our code
- we now have a function that can be passed down to a child Component as **props**

This concept of passing a function down to a child Component is how we lift data from a child to oa parent and a concept knows as **lifting state**.  This concept will be covered in another lecture. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

With our event handlers in place let's take a look at **React DevTools** 

If you highlight **Counter** it should look like the following:

<img src="https://i.imgur.com/hncbSl7.png" />

Now try incrementing the value a few times and you should see it update.

<img src="https://i.imgur.com/jSHBt5S.png" />

<hr>

### State Update Delay

Although the updates to state appear immediate there is one thing to note.  After calling **setCount** the new value assigned to state isn't available until the Component **re-renders**. 

So if we were to console log **count** immediately after it's been updated we would see it outputs the previous version of state. 

```js
const hanndleIncrement = () => {
    setCount(count + 1);
    console.log('handleIncrement - count:', count)
};
```

Here we can clearly see that **count** is now 2 but the console logs show that count is one value behind. 

<img src="https://i.imgur.com/V0agq9h.png" width=300/>

There will be instances where some logic needs to be run based on the new value stored in state but we can only do this after a re-render and it requires using the ** useEffect()** hook. 

The **useEffect** hook is a much broader topic and delves into the **React Component Lifecycle** methods, something we will learn about in upcoming lectures. 


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min

Let's try a quick activity that should help you apply some of these concepts.  

- Add a new **Reset** button to the Component
- Create a new **handler** function
- Inside the **handler** call **setCount** to update state 0

:thumbsup: - Click on the thumbs up when your done.

**Bonus**
- Try refactoring to include the callback function with SetCount.

```js
setCount((prevState) => prevState + 1);
```

<hr>

#### Final Solution

Here is the final version of the Counter Component.

<details>
<summary>Solution</summary>

<!-- ```js
import React, {useState} from 'react'

const Counter = () => {

  const [count, setCount] = useState(0)

  const handleIncrement = () => {
   setCount(count + 1)
  };

  const handleDecrement = () => {
    setCount(count - 1)
   };

  const handleReset= () => {
    setCount(0)
  };

  return (
    <div>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
        <button onClick={handleReset}>Reset</button>
      </section>
  )
}

export default Counter
``` -->

</details>



<hr>

#### :mag: - Check for Understanding 

Take a few minutes to think about the following questions:

  - Why does a react component need state?
  - What is the difference between **state** and **props** and provide an example of when to use each. 

**Note:** Do not slack your answers until the instructor has given the ok.

:thumbsup: Click on the thumbs up when your done.

When asked slack your answer(s) in a thread created by the instructor



<hr>

### Bonus - Using Conditional Logic and Ternary Operators

Since React is all JavaScript we can use all of our previous JS expertise when trying to implement additional, non React specific, logic. Let's take a look at the following:

- IF/ELSE
- Switch Statement
- Ternary Operator

Let's add some basic conditional logic to the **handleIncrement/handleDecrement** that will reset the count to 0 if it meets a specific threshold.  

#### IF/ELSE

```js
const handleIncrement = () => {
  if(count === 3) {
      handleReset()
    } else {
      setCount(count + 1)
  }
}
```
#### Switch Statements

Another form of conditional logic is to use a **switch** statement. They are the conditional logic of choice for the **useReducer** Hook.

For now let's refactor the code to use a switch statement. 
```js
const handleIncrement = () => {
   switch(true){
      case count === 3: 
        handleReset();
        break;
      default:
        setCount(count + 1)
    }
}
```

#### Ternary Operator

Most often React developers prefer to write a single if/else conditional as a **ternary** operator.  So let's perform our last refactor. 

**handleIncrement**
```js
const handleIncrement = () => {
  count === 3 ? handleReset() : setCount(count + 1)
}
```

**Final Working Solution:** [CodeSandbox](https://codesandbox.io/s/rctr-8-2-21-counter-starter-vi0nt?file=/src/Counter.js:782-831)


**State of Transition**

We are currently in a **state of transition** in world of React. Hooks were a game changer and have become the prefered way of writing Components React in 2021.  

Keep in mind however that there is way more code out there written in the previous syntax and any research you perform on React will almost certainly show Class based solutions unless you include the keyword **Hook** in your search query. 

**Instructor Demo**

> The instructor will perform a small demo of performing a Google search for updating state in React, with and without the keyword **Hook** 


### Resources

- [React Docs - useState](https://reactjs.org/docs/hooks-overview.html)
- [React Hook LifeCycle](https://wavez.github.io/react-hooks-lifecycle/)
- [The useState Hook - robinwieruch](https://www.robinwieruch.de/react-usestate-hook)
- [React useState Hook Guide - dmitirpavlutin](https://dmitripavlutin.com/react-usestate-hook-guide/)
- [React Event Handlers - robinwieruch](https://www.robinwieruch.de/react-event-handler)
- [ES6 Tutorial](https://www.javascripttutorial.net/es6/)
<hr>
