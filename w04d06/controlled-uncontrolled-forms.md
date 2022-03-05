<br>
Title: Controlled-Uncontrolled Forms<br>
Duration: 2hrs + <br>
Creator:  Joe Keohan<br>

---

# Controlled-Uncontrolled Inputs

<img src="https://i.imgur.com/BIes4H2.png" width=600/>

## Learning Objectives

After this lesson you will be able to:

- Implement a controlled and uncontrolled form
- Use the `useRef` Hook to reference an element
- Leverage the `onChange` event to capture and update live input


## Inputs...Inputs...Inputs

Inputs...inputs...are everywhere.  You can't escape them and they are a requirement for any site to capture user input.

Input elements are so important that there are close to 20 different types that can be assigned to them. Let's go over to [W3Schools](https://www.w3schools.com/tags/tag_input.asp) and take a look at a few fo them. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity -  We Do - 2min

Let's take a look at the top of [AirBnB's](https://www.airbnb.com/) landing page.  

<img src="https://i.imgur.com/hMcml6r.jpg" />

:question: - Where do you see inputs and what type are they?

<hr>



## Controlled vs Uncontrolled Inputs 

<!-- :walking: - The instructor will demo the differences between the following 2 login forms:

- AirBnB's 
- WordPress -->

**Controlled**

Some inputs are activated the moment you start typing and are considered to be **controlled**. A few examples of this are:

- the **location** field on AirBnB is one such type.  
- setting a [password field](https://4vlg9.csb.app/) that provides immediate criteria status

Depending on what characters you type, or the sequence of characters, there is some immediate response to the input.

**Uncontrolled**

Other inputs require that you first type all your info before it is captured and some action performed. 

This is an example of an **uncontrolled** input as it waits for the user to **submit** it's input `before it responds. 

A good example of an uncontrolled input is a [login form](https://w84fr.csb.app/)



## Uncontrolled Inputs

An uncontrolled input has less overhead as it waits until the user to type and then press submit.  Any control checks happen after the submit. 

<!-- Here is the starter code we will be working with: [CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-login-form-starter-forked-0v78f)  -->

Working with an uncontrolled input in React involves making use of the `useRef` Hook.  It's a Hook that allows us to `reference` an existing DOM element in order to grab some value or apply some property. 


### Starter Code

<!-- Start you server by doing the following:

- open your terminal
- cd into the [./student_examples/login-form-starter](./student_examples/login-form-starter) folder
- run **npm install** to install all dependencies
- run **npm start** to start the server -->

<!-- You can also choose to work on this codebase using this [CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-login-form-starter-forked-0v78f) -->

Here is the [CodeSandbox Starter](https://codesandbox.io/s/login-form-starter-0v78f)


### Uncontrolled inputs

We will first start with Uncontrolled inputs. 

<!-- CODESANDBOX STARTER -->
<!-- Here is the starter code we will be working with: [CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-login-form-starter-forked-0v78f)  -->



#### The `useRef` Hook

Uncontrolled inputs make use of the `useRef` hook which is used to create a reference to an existing DOM element.

Let's take a look at the [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html) 

#### Import `useRef` 

Like the `useState` Hook it must be imported from React. 

```js
import React, { useRef } from "react";
```

#### Create a New Instance of `useRef`
Once imported we create a new instance of `useRef`. 

``` js
const inputRefEmail = useRef()
```

Let's also include a console log to see what `useRef` returns. 


``` js
const inputRefEmail = useRef()
console.log('inputRefEmail - ', inputRefEmail)
```

In the terminal we should see the following:

<img src="https://i.imgur.com/teFzbUH.png" width=400/>

As we can see  it returns an object with a single key called `current`. 

Let's also take a look at `React DevTool` and see if shows up under the **hooks** section. 

<img src="https://i.imgur.com/yFZRZdx.png" width=500/>

#### Grabbing a Reference Using the `ref` prop
With **useRef** imported and a new instance created we now assign the ref to the DOM element we intend to reference.  

The `ref` is assigned as a `prop` with a value being the name of the ref we created earlier, in this case `inputRefEmail`. 

Let's assign this `ref` to the email field. 

```js
<input
    ref={inputRefEmail}
    type="text"
    className="form-control"
    name="email"
    placeholder="Email Address"
/>
```

Once assigned the previous console log will update to show that the current reference is the input.

<img src="https://i.imgur.com/fHHTFA4.png" width=400//>

Let's also take a look at `React DevTool` and see if anything has changed.

<img src="https://i.imgur.com/9QezGKs.png" width=500/>


#### Submitting the Input

Of course we now expect the user to type something and  to click the `login` button.  

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - You Do - 5min

It's your turn to apply your previous knowledge and attempt to set this up. 

This requires you do the following:

- Create a handler function and call it `handleSubmit`
- Add and `onClick` event to the button and assign the handler
- Add a console log inside `handleSubmit` to confirm it all connected

:thumbsup: - Click on the thumbs up when you've implemented the solution

<hr>

<!-- Solution Steps Here... -->

<details><summary>Solution</summary>

```js
```
</details>

In this case we will call the function `handleSubmit` since it's being used to submit the input.   

For now let's also add a console log to confirm the handler is being executed. 

```js
const handleSubmit = () => {
    console.log('handleSubmit')
}
```

And now assign the `onClick` to the submit button. 

```js
<button 
    onClick={handleSubmit} 
    className="btn btn-lg btn-primary btn-block">
    Login
</button>
```

Time to test out the design.  Try clicking the button and confirm we wee the console log output.  

</details>



#### Grabbing The Input

Since we know that `useRef` allows us to reference to the `input` let's console log the .current` key as well. 


```js
const handleSubmit = () => {
    console.log('handleSubmit', inputRefEmail.current)
}
```

<img src="https://i.imgur.com/2ku0wb0.png" />

The way we now return the value stored in the input is to use the **value** key. 

```js
const handleSubmit = () => {
    const value = inputRefEmail.current.value
    console.log('handleSubmit - value', value)
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - You Do - 5min

Now it's your turn to try. 

- Create another instance of `useRef` called `inputRefPassword`
- Assign it to the password input element
- Console log the captured value in `handleSubmit`

:thumbsup: - Click on the thumbs up when you've implemented the solution

<hr>

One last thing we need to do is to clear the input fields when the user submits the form. 



```js
inputRefEmail.current.value = ''
inputRefPassword.current.value = ''
```

#### Adding State

We still need to capture the user input and store it in state.  State can reside in either this Component or lifted up it's parent. 

Let's import the **useState** hook. 

```js
import React, { useState, useRef } from 'react'
```

We now consider the following options for creating state:

- create multiple instance of state, one for each input
- create a single instance of state to hold both values.  

Let's opt for the second option and create a single instance of state and assign it an object with key names that correspond to the input we are capturing. 

```js
const Form = (props) => {

  const [login, setLogin] = useState({email: '', password: ''})
  console.log('login -', login)
  //...rest of code
}
```

Refreshing the page will display the state in the console.

<img src="https://i.imgur.com/PLfnZ6h.png" width=400/>


Let's also take a look at `React DevTool` and see if anything has changed.

<img src="https://i.imgur.com/V9sr91n.png" width=500/>

#### Updating State

Now let's update the state value once the button is submitted. 

```js
const handleSubmit = () => {
    setLogin({
        email: inputRefEmail.current.value,
        password: inputRefPassword.current.value
    })
};
```

Once the button is clicked React DevTools will reflect the change in state. 

<img src="https://i.imgur.com/xQszWyG.png" width=700/>


## Controlled Inputs

Controlled inputs require a bit more setup than their uncontrolled counterparts.  Essentially state needs to be updated with each and every user keystroke so that we can perform some immediate action for each input.

Let's first update App to import and use the other form. 

```js
// import Form from './FormUnControlled'
import Form from './FormControlled'
```

Some of the configuration needed for this form is identical to the other so let's give you a chance to apply your skills. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - You Do - 5min

- Import `useState` and set it up as we did before
- Create and setup `handleSubmit` as we did before
- Confirm that the `handleSubmit` button works by, you guessed it, adding a console log

:thumbsup: - Click on the thumbs up when your done.

<hr>

#### Controlling The Input

Controlling the input requires that state be updated with each keystroke. 

In order to do this we need to do the following:

- add a `value` prop to both inputs and assign it a corresponding state value
- add an `onChange` event to each input that will be triggered with each key stroke
- create a new `handler` function for the `onChange` event 

#### Assigning a Value Prop

Let's assign a `value` prop to each input. 

```js
// EMAIL INPUT
<input value = {login.email} />
// PASSWOORD INPUT
<input value = {login.passsword} />
```

Now try typing into those inputs on the screen again. 

What you will notice is that none of your input is displayed on the screen as you type into those fields. 

The reason is that the inputs are assigned values based on the current state value, which at this point is an empty string for both fields. 


#### Setting up the Handler and onChange Event

In order to capture every keystroke we need to add an `onChange` event listener to both inputs and assign the corresponding handler function.

Let's first create the handler.  One thing to consider now is that we are no longer using `useRef` to grab a reference of the input so we need another way to distinguish which input called the function.  

We will do so by referencing the `event` objects `target` property.  

This means adding a parameter to handleChange that will pass in the event object. 


```js
const handleChange = (event) => {
    console.log('handleChange - event', event)
}
```

Let's now we assign the handler to both inputs. 

```js
onChange={handleChange}
```

Try typing a sequence character in the email field and you should see the characters displayed in the console.

<img src="https://i.imgur.com/LrWr71O.png" />

Expanding any one of the event objects will show over 2 dozen keys but the one we are interested in is `target` as it shows the target element of the event.

<img src="https://i.imgur.com/7wZoY3J.png" width=300/>

#### Capturing the Input Value

Inside of `handleChange` we can now grab the input value using  `event.target.value`. 

```js
const handleChange = (event) => {
    console.log('handleChange - event', event.target.value)
}
```

Now type in a sequence of characters and we should see just that input. 

<img src="https://i.imgur.com/jNPnZi1.png" width=300/>

Here is the thing though. `handleChange` is being used to capture input for both fields.  We can confirm this by adding another console log that targets: 

```js
console.log('handleChange - event', event.target.name)
```

Clicking once in each field will return the following console output.

<img src="https://i.imgur.com/pbUsvae.png" width=400/>

Let's move onto updating state and see how we can work out the logic to update the appropriate  fields. 

#### Updating State

Since state has been assigned an object we will need to update the key that corresponds to the correct input. We could do so by running some conditional logic based on the previous `event.target.name` values but there is a more efficient way to do this. 


**Dynamic Object  Keys**

Since we assigned both inputs the same name values as the keys in state we can use that to our advantage. 
```js
// INPUT
name="email"
// STATE
const [login, setLogin] = useState({email: '', password: ''})
```

 We first create a variable that grabs the value of the targets name and then use that as the value for the key name in state. 

```js
const handleChange = (event) => {
    const name = event.target.name
    setLogin({  
        [name]: event.target.value
    })
}
```

If we type several characters in sequence we should see them remain in the input field as well as being updated in state. 

<img src="https://i.imgur.com/df7JiQi.png" width=300/>

So the following two things occured:

- state now only contains a single key of email 
- and the following warning appeared just once

<img src="https://i.imgur.com/Rnan7FT.png" />

:question: - Question: How do we fix the issue with state? 


#### Object Destructuring

The answer is to import all keys that exist in state and then update the key(s) we need to as this time. 
```js
const handleChange = (event) => {
    const name = event.target.name

        setLogin({  
        ...login,
        [name]: event.target.value
    })
}
```

Doing so will capture both inputs and update state

<img src="https://i.imgur.com/hyMMmMI.png" width=400/>

### Bonus #1- Working With `<form>` Elements

If time permits the instructor will perform a codealong/demo of updating the `Form` Component to include a `<form>` element which makes use of the `onSubmit` event.


<!-- 
For now we are only going to comment out the `setLogin` code in there as you will be working out this logic in the lab. -->

<!-- ### Bonus #2- Lifting State

If time permits the instructor will perform a codealong/demo of lifting state and conditional rendering the `Form` Component 
-->


<!-- 
[Solution CodeSandbox](https://codesandbox.io/s/rctr-9-8-20-login-form-in-class-demo-b3hiz?file=/src/components/App.js) -->

[Solution CodeSandbox](https://codesandbox.io/s/login-form-starter-rctr-8-2-21-oeumy?file=/src/components/App.js:602-638)

<!-- ### Lab Time

The instructor will provide the lab -->
