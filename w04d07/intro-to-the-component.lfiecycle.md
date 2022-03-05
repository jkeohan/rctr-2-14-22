<br>
Title: Component LifeCycles<br>
Duration: 1hr + <br>
Creator:  Joe Keohan<br>

---

# The Component LifeCycles

## Prerequisites

- React
- Components
- State and props

## Learning Objectives

After this lesson you will be able to:

- Explain the 3 phases of the Component lifecycle
- Use `useEffect` to implement code in each of the 3 main lifecycle methods

## Framing

So far we've learned that React Components can be used to break down the UI into smaller and smaller bit of reusable functionality. The Component model even encourages going as low level as rendering a single button.

Part of the Component `reusability` design is that it allows them to contain as much logic as needed to adapt to their environment and implementation. That flexibility might require the Component to perform some action when it's first `mounted`, then `updated` and perhap, even when it's `unmounted`.

Take for instance AirBnB. When you perform a search, the site returns a set of data points that match the query and must update state in some way in order to render those items as Components.

The Components themselves may need to keep track of if, and when, it's been added as a favorite :heart: or adjust it's own layout based on `mobile` or `tablet` layout.

<img src="https://i.imgur.com/nCZVlLs.jpg" />

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

Let's take a look at the following versions of the Mars website that I built in React.

- [Mars - Media Queries](https://0wqnv.csb.app/)
- [Mars - Inline Styles](https://wpixk.csb.app/)

Let's do the following together:

- Open both sites in separate tabs and with DevTools open as well.
- In DevTools use the `Toggle Device Toolbar` to view the site in Responsive mode
- Enable `Tablet` view for both web sites
- Select and examine the following element:

```html
<div id='nav_container>...</div>
```

The Instructor will now direct your attention to those elements the difference between the two apps.

**Note:** The implementation of these two sites were created for the following medium article I wrote on [3-ways-to-implement-responsive-design-in-your-react-app](https://medium.com/@jkeohan/3-ways-to-implement-responsive-design-in-your-react-app-bcb6ee7eb424)

<hr> -->

## The 3 Main Phases Of The Component Lifecycle

As the complexity of the Component grows we can make use of more and `Hooks` to meet the demands of our business logic. Certain functionality might need to be performed only once when Component loads or with each re-render.

Below are the 3 phases that a Component goes through during it's lifetime.

- Mounting
- Updating
- Unmounting

`Mounting` and `Unmounting` occur only once during the lifecycle of the Component with `Updating` occurring as often as the Component is re-rendered.

Each phase can call a specific `lifecycle method` that runs as the last function call in that cycle.

Here are diagrams that convey the lifecycles as they apply to Classes Components.

<img src="https://i.imgur.com/eNlBcr8.png" />

Here are diagrams that convey the lifecycles as they apply to Hook based Components.

<img src="https://i.imgur.com/arj7aZD.png" />

<!-- Although up to this point we've only worked with `Functional` Components, in lue of `Classes`, however under the hood React is indeed initializing and calling them as if they were written as classes.  -->

The table below shows the corresponding way to make use of the **useEffect** hook to implement the class based LifeCycle methods.

| Phase      | useEffect | Class Method 
| ----------- | ----------- | ----------- |
| Mounting     | useEffect(() => {}, []) |  ComponentDidMount    |
| Updating  | useEffect(() => {})       | ComponentDidUpdate
| Updating  | useEffect(() => {}, [someValueToMonitor])     | ComponentDidUpdate but only if value changes
| Unmounting | useEffect(() => { return () => { } })       | ComponentWillUnmount

<!-- **Mounting:** called when a component is created and inserted into the DOM. -->

<!-- - **function** - initializes the component
- **`return()`** - `returns` the UI
- **DOM and Refs** - done using `useRef`
- **useEffect** - performed using `useEffect(() => {}, [])`

**Updating:** usually triggered by changes in props or state.

- **setState() function** - updates state which triggers the re-render
- **`return()`** - `returns` the UI
- **DOM and Refs** - done using `useRef`
- **useEffect** - performed using `useEffect(() => {})` (No [] included)
- **useEffect** performed using `useEffect(() => {}, [someValueToMonitor])`

**Unmounting:** called when a component is being removed from the DOM.

- **useEffect** - `useEffect(() => {})` (No [] included) -->

## The `useEffect` Hook

Now it's time to add yet another Hook to our collection, the useEffect Hook. This Hook lets us perform `side effects` in functional components.

> A side effect is any application state change that is observable outside the called function other than its return value.

Several examples of `side effects` are:

- Logging to the console
- Making an API call
- Calling setInterval/setTimeout

As we pointed out during the overview of the React lifecycle, `useEffect` and be run in one of 3 ways:

- `useEffect(() => {}, [])` - empty [] means this will only run once when the Component mounts
- `useEffect(() => {})` - no [] means this will run on every render/re-render
- `useEffect(() => {}, [someValueToMonitor])` - run on mount and then only if the value has changed

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

#### Starter Code

Here is the starter code we will be working with: [CodeSandbox Starter](https://codesandbox.io/s/useeffect-starter-forked-t9j5u?file=/src/Counter.js)

<!-- Here is the starter code we will be working with: [odeSandbox Starter](https://codesandbox.io/s/useeffect-starter-9cpw0?file=/src/Counter.js)  -->

:thumbsup: - Click on the thumbs up when you have forked the starter code.

<hr>

### Mounting

Since every Component requires an initial mounting it makes sense that we start with the `mounting` phase.

Let's take a look at the [Solution](https://9mdkb.csb.app/) we are looking to implement. As we can see the app does the following:

<!-- https://codesandbox.io/s/useeffect-starter-9cpw0?file=/src/Counter.js -->

- timer starts counting when the Component mounts
- timer increments every second
- clicking on the `pause` button pauses the timer
- clicking on `start` re-initiates the counting sequence.

Implementing this type of functionality requires that we make use of the  `useEffect` Hook.

But let's first push the envelope and see how far we can go without `useEffect` before we hit our first wall.

**Base Functionality**

As of right now our implementation only contains the console logs needed to confirm that the buttons work.

```js
const Counter = () => {
	const [count, setCount] = useState(0);
	let interval = null;

	const startTimer = () => {
		console.log('startTimer');
	};

	const pauseTimer = () => {
		console.log('stopTimer');
	};

	return (
		<>
			<div>Counter: {count}</div>
			<button onClick={startTimer}>Start Timer</button>
			<button onClick={pauseTimer}>Pause Timer</button>
		</>
	);
};
```

### Increment The Counter On Mount

Let's first see if we could at least call `startTimer` when the component is loaded. That's easy to do as we only need to call the function. For now let's put it just above the `return` statement.

```js
startTimer()

return (
    // ...rest of code
)
```

So it seems calling `startTimer()` when the Component loads does indeed execute the function.

Now let's add the logic `startTimer` that will increment the counter just once when it's mounted.

```js
const startTimer = () => {
	console.log('startTimer');
	setCounter(counter + 1);
};
```

React doesn't like that very much and errors out as it takes us to brink of an infinite loop.

<img src="https://i.imgur.com/IfesZpZ.png" width=400/>

**Note:** Make sure to delete calling `startTimer()`.

:question: - Why the error?

<details><summary>Answer</summary>

Calling `startTimer()` updates state which triggers the Component to update, which then calls the function again triggering another update..and so on..

</details>

### ComponentDidMount - Run Once On Mount

So we need a means of calling `startTimer()` when the Component is initially mounted but not on any subsequent re-renders. For that use case we make use of the **useEffect** hook.  


Since `useEffect` is a hook it needs to be imported.

```js
import React, { useState, useEffect } from 'react';
```

We will implement **useEffect** in the following way:

```js
useEffect(() => {}, [])
```



`useEffect` takes in a callback function as it's first param and an array (optional) `[]` as its second parm. The empty `[]` is how we tell `useEffect` to run only on the initial mount.

```js
useEffect(() => {
	console.log('useEffect');
	startTimer();
}, []);
```

#### Adding a SetInterval

Ok. So now we have a means of calling it a single time. That's enough to to get us started and now we can add the additional logic `setInterval` logic to increment every second.

This also bring us to the following best practice:

:star: - Use the callback function version of useState if you need to reference the previous version of state.

Since `setCounter` is being called in the callback function of `setInterval` this is a perfect use case for using the callback version of `setCounter`

```js
const startTimer = () => {
	console.log('startTimer');
	interval = setInterval(() => {
		console.log('setInterval');
		setCounter((prevState) => prevState + 1);
	}, 2000);
};

const pauseTimer = () => {
	console.log('stopTimer');
	clearInterval(interval);
};
```

This seems to do the trick and were back on track with the Counter app. Now let's work out the logic to pause the timer.

### Pausing The Timer

With 2 of the app requirements in working order let's see if we can pause the timer. Clicking on `Pause Timer` does indeed execute the function, as seen in the console logs, but does nothing to stop the timer.

If we also click on `Start Timer` a few times in a row we will see that it increments several times and begins to jump ahead.

#### ComponentWillUnmount

One thing that hasn't been mentioned yet is that every time a re-render happens, we create a new effect replacing the previous one. Although in our use case `useEffect` isn't being called there is still a need to clear the interval just before the re-render. This falls ito the category of `ComponetWillUnmount`

React must clean up the previous effect before applying the next effect. In our case we need to remove the previous instance of the `setTimer` and create a new instance.

For this we need to refactor `useEffect` to do the following:

- it must clear the previous `setInterval` before the new instance of `useEffect` is called

To do this we add a final `return` statement that is passed a callback function.

```js
useEffect(() => {
	console.log('useEffect');
	startTimer();
	return () => clearInterval(interval);
}, []);
```

#### ComponentDidUpdate

This doesn't seem to do the trick. Thats because we need to run `useEffect` on every re-render or when the `ComponentDidUpdate`. In order to do that we remove the `[]`.

```js
useEffect(() => {
	console.log('useEffect');
	startTimer();
	return () => clearInterval(interval);
});
```

#### ClearInterval Once More

Even with this implementation were still faced with the same problem that multiple clicks to `Start Timer` will cause the timer to count much faster.

In order to resolve this we need to add one more `clearInterval` to `startTimer` to clear out any timer that was initiated before the next interval value.

```js
const startTimer = () => {
	clearInterval(interval);
	//...rest of code
};
```

Here is good summary for implementing `useEffect`.

<img src="https://i.imgur.com/ViLj2qG.png" width=700/>

### Bonus - Conditional Rendering A Component

A much better UI for our Counter would be to show only 1 button at a time. We essentially would toggle between the buttons with only one of them being visible at any one time.

Enabling this functionality would also require a bit of refactoring of our code which is beyond the scope of this bonus so we will only focus on how to conditionality render the buttons.

**More State**

First let's add an additional state value.

```js
const [toggle, setToggle] = useState(false);
```

**Ternary Operator**

Now we can add the conditional logic needed to toggle between the buttons. We will do this using a `ternary operator`.

```js
return (
	<>
		<div>Counter: {counter}</div>
		{toggle ? (
			<button onClick={startTimer}>Start Timer</button>
		) : (
			<button onClick={pauseTimer}>Pause Timer</button>
		)}
	</>
);
```

**Complete Refactor**

Here is the code that includes the complete refactor and the [CodeSandbox Solution](https://codesandbox.io/s/useeffect-solution-9cpw0)

<details><summary>Solution</summary>

```js
const Counter = () => {
	const [counter, setCounter] = useState(0);
	const [toggle, setToggle] = useState(false);

	useEffect(() => {
		let interval;
		if (!toggle) {
			interval = setInterval(() => {
				setCounter((prevState) => prevState + 1);
			}, 2000);
		}
		return () => clearInterval(interval);
	}, [toggle]);

	const handleToggle = () => {
		setToggle(!toggle);
	};

	return (
		<>
			<div>Counter: {counter}</div>
			{toggle ? (
				<button onClick={handleToggle}>Start Timer</button>
			) : (
				<button onClick={handleToggle}>Pause Timer</button>
			)}
		</>
	);
};
```

</details>

### References

- [React Hooks Lifecycle](https://medium.com/@galmargalit/react-function-components-hooks-lifecycle-diagram-14f76e0a5988)
- [Replacing Component Lifecycle Methods with React Hooks](https://blog.carbonfive.com/replacing-component-lifecycle-methods-with-react-hooks/)
- [Effects Shouldn't Lie About Their Dependencies](https://medium.com/@5066aman/effects-shouldnt-lie-about-their-dependencies-44becff15582)
- [3-ways-to-implement-responsive-design-in-your-react-app](https://medium.com/@jkeohan/3-ways-to-implement-responsive-design-in-your-react-app-bcb6ee7eb424)
- [build-a-react-timer-component-using-hooks](https://upmostly.com/tutorials/build-a-react-timer-component-using-hooks)
- [setinterval-in-react-components-using-hooks](https://upmostly.com/tutorials/setinterval-in-react-components-using-hooks)
