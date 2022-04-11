<br>
Title: Custom Hooks<br>
Duration: 1 - 1.5hrs <br>
Creator:  Joe Keohan<br>

---

# Custom Hooks

## Learning Objectives
- Create custom Hooks that can be reused in different apps
- Use state to keep track of data within the Hook
- Include useEffect's to manage the Hooks lifecycles

## Framing

As with any project there comes the observation that the same snippets of code are being used in separate parts of the code base.  This realization then drives the decision to structure that code into a reusable format so that it can be used whenever and wherever needed.  

Let's jump into the way back machine to week 1 when we learned about Components and used them to recreate [Bootstrap Cards](https://codesandbox.io/s/rctrr-8-8-20-bootstrap-solution-uyvmg?file=/src/App.jshttps://codesandbox.io/s/rctrr-8-8-20-bootstrap-solution-uyvmg?file=/src/App.js)


Recreating the Bootstrap Cards in React began with creating 2 separate Components with the same structural content but different prop values.

```html
<Card1 title="Santorini" img="image" text="some text" url="some url"/>
<Card2 title="Zakynthos" img="image" text="some text" url="some url"/>
```

Seeing this pattern and knowing it  wouldn't be practical to use it to create 100+ cards drove us to refactor into a single component that would allow us to create as many cards as were in the dataset. 

```html
const cards = cardsArr.map((ele, index) => {
  return (
    <Card img={ele.img} title={ele.title} text={ele.text} url={ele.url} key={index}/>
  );
});
```

This ***reusability*** aspect is something we all strive for when developing code. 

<!-- Here is an [additional example](https://codepen.io/jkeohan/pen/ZPJPrB?editors=0010) but specifically for jQuery. -->

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

In your dev career what functionality have you come across that you say the saw a use case to refactor into a reusable function and/or Class and then incorporate into other apps? 

Take 2 min :clock1: to think about it and then post your answer in the thread. 

<hr> -->

<!-- So it looks we might already have a few use cases for custom Hooks.  -->

### Custom Hooks

In the world of React ***Custom Hooks*** are meant to be flexible enough to be reused in many more apps then the one you are working on at this moment.  In order to do this we must follow the rule of: ***standard input = standard output***.

What makes Custom Hooks unique is that they can leverage any of the existing Hooks, such as ***useState***, ***useEffect***, ***useRef***, ect along with any additional functionality needed. 

### Custom Hook Configurations

As you begin working out the functionality of your custom hook you will also need to consider the following:

- which React hooks to include 
- what needs to be passed and exported from the function

Some custom Hooks leverage only ***useState***, while others include ***useEffect***.  Some some may require both or replace ***useState*** with ***useReducer***.  

#### LocalStorage Hooks
Let's take a look at the following example of [useLocalStorageState by Gabe Ragland](https://usehooks.com/useLocalStorage/) that makes use of ***localStorage*** and returns what we would expect from **useState**.


```js
const [count, setCount] = useLocalStorageState('countApp', 0)
setCount(count + 1)
```

Here is another [useLocalStorage Hook](https://www.npmjs.com/package/@rehooks/local-storage) but with some added functionality that allows the user to delete the ***localStorage***. 

```js
const [ name, setName, deleteName ] = useLocalStorage("name")
setName("localStorageName")
deleteName()
```
<!-- [useLocalStorage by @rehooks](https://www.npmjs.com/package/@rehooks/local-storage) -->

<!-- #### useArray Hook

Here is a different example of a custom Hook that returns a single custom object with methods that seek to emulate the Array ***push*** and ***splice*** methods along with removing all the previous elements altogether. 

```js
const todos = useArray([])
todos.add('learn hooks')
todos.remove('learn hooks')
todos.clear())
```

[useArray by Aayush Jaiswal
](https://blog.bitsrc.io/writing-your-own-custom-hooks-4fbcf77e112e) -->

### Our First Custom Hook - useDocumentTitle
Let's take a look a really basic example of a Counter Component that also updates the ***document.title*** of an open tab with text that display the current ***count*** value. 

**Stater CodeSandbox:** [useDocumentTitle](https://codesandbox.io/s/custom-hooks-starter-egwjy?file=/src/Counter.js)

It's not currently using any Custom Hooks but that will change once we evaluate what can be removed and placed into our new hook.

```js
const Counter = () => {
  const [count, setCount] = useState(0)
  const handleIncrement = () => setCount(count + 1)

  useEffect(() => {
      document.title = `You clicked ${count} times`
  }, [count])

  return (
    <>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
      </section>
    </>
  );
};

export default Counter
```

In this example it's clear that ***useEffect*** is being called on ***componentDidUpdate*** but only when the ***[count]*** dependency value changes. 

```js
useEffect(() => {
    document.title = `You clicked ${count} times`
}, [count])
```

Let’s remove the ***useEffect*** section out of the component and place it inside a new file called ***useDocumentTitle.js***.  

<!-- Once the file is created let's create a new function which we will call ***useDocumentTitle***.   -->

The function's only task is to update the ***document.title*** if the title has changed.  

```js
const useDocumentTitle = title => {
  useEffect(() => {
      document.title = title
  }, [title])
}

export default useDocumentTitle
```

Now we can use this new custom Hook in the Counter Component. 

```js
import useDocumentTitle from './useDocumentTitle'

const Counter = () => {
  const [count, setCount] = useState(0)
  const handleIncrement = () => setCount(count + 1)
  const title = `You clicked ${count} times`
  useDocumentTitle(title)

  return (
    <>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
      </section>
    </>
  );
};

export default Counter
```

This might seem like a useless Hook but the functionality it provides is used quite often.  Take for instance how Facebook uses it to notify the user as to new or unread messages. 

<img src="https://i.imgur.com/rMh4uiO.png" width=300/>

<br>
<br>

**Solution CodeSandbox:** [useDocumentTitle](https://codesandbox.io/s/rctr-9-8-20-counter--usedocumenttitle-solution-4dcci)

### The Local Storage Hook

Let's take a look at the first local storage example and build it together. The functionality we are looking to achieve with this Hook is the following:

- create and set localStorage to some value
- return and update the value from localStorage 

#### Which React Hooks To Use
Now it's time to consider which of the React Hooks it would need to perform this functionality. 

Here is how it would be initialized and considering that it returns what looks like ***useState*** values I'm sure it's safe to assume that it includes ***useState***.  

```js
const [count, setCount] = useLocalStorageState('countApp', 0)
setCount(count + 1)
```

<!-- **Stater CodeSandbox:** [Counter useLocalStorage Hook Starter](https://codesandbox.io/s/rctr-9-8-20-counter-starter-localstorage-egwjy?file=/src/Counter.js) -->

First let's create a new file called **useLocalStorage.js** and add the following:

```js
import React, {useState, useEffect} from 'react'

export default function useLocalStorage(key, defaultValue) {
  const [state, setState] = useState()

  return [state, setState]
}
```

With our basic structure in place lets see if we can implement the following features:

- create and set localStorage to some value
- return that value from localStorage

Here we will use a callback function when setting the initial state which will retrieve the localStorage if it already exists or 

```js
import React, {useState, useEffect} from 'react'

export default function useLocalStorage(key, defaultValue) {
  const [state, setState] = useState(() => {
    try {
      const value = localStorage.getItem(key)
      return value ? JSON.parse(value) : defaultValue
    } catch(e) {
      console.log('e', e)
      return defaultValue
    }
  })

  return [state, setState]
}
```

Since **state** is initialized once we will need additional logic to update **localstorage** when the state value changes. 

This sounds like a good use case for adding a ***useEffect***, including it's ***[dependency]*** array.  When the dependency value changes this would then trigger ***useEffect*** to run at which time we can set the value to ***localStorage***

```js
export default function useLocalStorage(key, defaultValue) {
  const [state, setState] = useState(() => {
    try {
      const value = localStorage.getItem(key)
      return value ? JSON.parse(value) : defaultValue
    } catch(e) {
      console.log('e', e)
      return defaultValue
    }
  })

  useEffect(() => {
    localStorage.setItem(key, state)
  }, [state])

  return [state, setState]
}
```

**Solution CodeSandbox:** [Counter useLocalStorage Hook Solution](https://codesandbox.io/s/rctr-9-8-20-counter-solution-localstorage-nsqe0?file=/src/Counter.js)


## Custom Hooks Abound

 Since the release of the React Hooks, there has been an explosive growth of custom hooks.  Thousands of React devs from all over the world have churned out custom hooks that simplify most of the arduous and boring tasks we do in React projects.

Here are some resources that provide custom hooks or walk you through the process of creating them yourself. 

- [useLocalStorage Hook](https://usehooks.com/useLocalStorage/)
- [useHistory Hook For React Router](https://medium.com/javascript-in-plain-english/navigating-your-react-app-with-the-usehistory-hook-c7c465bfc6f6)
- [Writing Your Own Custom Hooks](https://blog.bitsrc.io/writing-your-own-custom-hooks-4fbcf77e112e)
- [11 Custom Hooks](https://blog.bitsrc.io/11-useful-custom-react-hooks-for-your-next-app-c66307cf0f0c)