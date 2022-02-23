<br>
Title: Passing Props<br>
Duration: 1 hr+ <br>
Creator:  Joe Keohan<br>

---

# Intro To Props

## Learning Objectives

- Cover the rules that govern how props are used
- Create and pass props to Components
- Loop over an array of objects that then returns a Component for each object
- Work with additional JSX rules

## Framing

Having worked with functions we know that they are meant to be reusable.

The reusability of a function is in it's ability to accept arguments, perform an action and return a predictable value.

`Standard Input` produces `Standard Output`

Now consider that our application contains many Components, some of which may require data points in order to render the UI. Being that we are writing **Functional Components** it makes sense that they will accept arguments and return UI based on the data passed.

The data we pass from a `parent > child` Component are called: `props`.

React data flow is `unidirectional` and can only be passed down, and never from `child` to `parent` or `sibling` to `sibling`.

### Props

Every Component has a `props` object even if no data has actually been passed.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's revisit our previous [Bootstrap Cards](https://codesandbox.io/s/bootstrap-starter-props-ryh02d?file=/src/App.js) in `React Developer Tools` see if anything `props` related pops out.

<!-- STARTER
Starter from last session 
https://codesandbox.io/s/seir-628-bootstrap-starter-props-llbeh?file=/src/CardImage.js

Original Card Starter
https://codesandbox.io/s/components-bootstrap-starter-o2ry1?file=/src/App.js
-->

<!-- SOLUTIONS -->
<!-- https://codesandbox.io/s/seir-831-bootstrap-solution-r8p9i?file=/src/App.js 

[Bootstrap Cards](https://codesandbox.io/s/components-bootstrap-starter-forked-2bujt?file=/src/App.js)

[Bootstrap Cards](https://codesandbox.io/s/rctr-8-2-21-components-bootstrap-starter-forked-d484q)
-->

If we highlight the `Card1` Component we will see something called `props` in the right pane.  As a matter of fact, if you highlight any Component you will see the same `props` reference. 

<img src="https://i.imgur.com/qzpnB0y.png" /><br>

Since we haven't yet passed any data to these Components the props object contains no values.

**End Goal**

Let's take a look at the final [solution](https://d484q.csb.app/) and compare how much more data props contains.

<!-- SOLUTION for d484q -->
<!-- https://codesandbox.io/s/rctr-8-2-21-components-bootstrap-starter-forked-d484q?file=/src/App.js -->

<!-- WITH FOLDERS -->
<!-- Here is the [Final Solution](https://codesandbox.io/s/bootstrap-solution-seir-1207-2v48i?file=/src/App.js) -->

<!-- WITHOUT FOLDERS -->
<!-- Here is the [Final Solution](https://codesandbox.io/s/seir-831-bootstrap-props-starter-zeuwb?file=/src/App.js:72-76) -->

<img src="https://i.imgur.com/nFaRt0E.png" />

#### React Architecture

This is the current React architecture and represents all the Components and their relationship in the hierarchy.

<img src="https://i.imgur.com/y2BR5wK.png" >
<hr>

### Prop Rules

Let's extend the rules we defined previously for Components and JSX to now include `props`.

:oncoming_police_car: - Props adhere to the following rules:

- Data is unidirectional passed down from a `parent` > `child`
- All **Props** passed to a child are organized into a single object in the child Component
- Props are **immutable** and cannot be reassigned a new value within the child Component

This Rule isn't regarding props but something we will need to keep in mind going forward:

- Any Components created using **Array.map()** must be assigned a **key** prop with a unique value.

### Passing Props

Say for instance we wanted to render the destination name that the image represents in our cards. We could go directly to **CardBody** and do the following:

```html
<h5 class="card-title">Santorini</h5>
```

This is a fairly manual process and doesn't scale well and isn't dynamic.

#### Understanding Props In General

A **prop** is written as a **name=value** format like all other HTML attributes such as:

```html
<!-- The src property of a image tag -->
<img src="someurl" />
<!-- The class property assigned to any element -->
<div class="container"></div>
<!-- The href property assigned to an anchor tag -->
<a href="someurl"></a>
```

Since the `Card1` component is the parent that renders `CardBody` than it must pass the prop to it's child.

:oncoming_police_car: - Data is unidirectional in React passed down from a `parent` > `child` Component

#### Creating And Assigning A Prop Value

Inside of our **Card** Component let's assign **CardBody** the following `prop`.

```js
<CardBody title='Santorini' />
```

Nothing will change as CardBody has not yet been configured to use that prop. 

#### Accepting Props

The **CardBody** Component will now be updated to to accept the incoming props. The first thing we need to do is add the keyword **props** as a parameter.

Let's make sure that **CardBody** is being passed the `title` prop by adding a console.log.

```js
const CardBody = (props) => {
	console.log('this is props:', props);
	// ...rest of the code
};
```

In DevTools you should see the following in the console.

<img src="https://i.imgur.com/HlrtO2T.png" width=300/>

We can see here that `props` is an object and that `title` is a key. This will be the same pattern for when we start passing in multiple props. Each prop passed will be assigned as a unique **key:value** pair.


#### Props Are Immutable

:oncoming_police_car: - Props are immutable which means we can't reassign them a new value within the receiving Component.

Let's take a moment to confirm this and open the `CardBody` Component and add the following:

```js
// ORIGINAL VALUE OF TITLE
console.log('current props.title', props.title);
// ATTEMPT TO REASSIGN TITLE A NEW VALUE
props.title = 'Mykonos';
console.log('new props.title', props.title);
```

Refresh the page and you should see the following:

<img src="https://i.imgur.com/Nmio71o.png" width=300/>

It looks like props was not updated to reflect the edit. So any attempt to change those props directly within the Component will have no effect.



#### Using Props

Let's now replace the hard coded value for title to the one being passed down as props. 

:oncoming_police_car: - Any JavaScript code that needs to be executed in JSX must be enclosed in opening/closing curls braces `{}`

```js
<h5 className='card-title'>{props.title}</h5>
```

### Passing Mulitple Props

We could do the same for all the additional values we wish to pass but as you can imagine if we had 10, 20, 100+ cards this manual method becomes completely inefficient.

Also it is more likely that the data we will be using to render the cards will be imported either via a file or returned from an API call.

Either way we should expect that if we will need to create multiple cards that the card data will be stored as an array of objects: `[{}, {}]`

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's use some real data which we will use to replace the generic placeholder text.

- Create a new file in `src` called `cardData.js`
- paste the following code into the file

```js
export default [
	{
		img:
			'https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60',
		title: 'Santorini',
		text:
			"This was one of the most amazing places I've ever seen. A must see for eveyrone",
		url: 'https://unsplash.com/s/photos/santorini',
	},
	{
		img:
			'https://images.unsplash.com/photo-1498712964741-5d33ab9e5017?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=600',
		title: 'Zakynthos',
		text:
			'This was like being a pirate and we were looking to bury our treasure. It was so isolated and beautiful. ',
		url: 'https://unsplash.com/s/photos/zakynthos',
	},
];
```

- Import the data into `App.js` as `cardsArr` and add a **console.log** to confirm it was imported.

```js
// IMPORT DATA
import cardsArr from './cardsData';
console.log('this is cardsArr:', cardsArr);
```

:thumbsup: Click on the thumbs up when your done.

<hr>

#### Creating Multiple Cards

With the data in hand we can now loop over the array and render as many `Card Components` as their are objects in the array, passing them the `props` needed for each card.

Inside of the `App` Component we will loop over the `cardsArr` array and create a `Card` for each object in the array.

Each prop is defined on it's own and passed a corresponding value.

Let's also console the `cards` so see what React magic has been performed.

```js
const cards = cardsArr.map((card, index) => {
	return (
		<Card1 
			img={card.img} 
			title={card.title} 
			text={card.text} 
			url={card.url} 
		/>
	);
});

console.log('this is cards:', cards);
```

Now take a look in DevTools and you should see the following:

<img src="https://i.imgur.com/gx42Kme.png" />

Each object appears to contain much more info then we passed as well as each one contains a `$$typeof` key that is set to `Symbol(react.element)`. 

<!-- `Symbols` were a new primitive data type introduced in ES6 and are unique, meaning if we create many Symbols with the same value they will be unique.  -->

In order for React to distinguish each element and manage updating it in the **Virtual DOM** it must be unique.  This is done by assigning a new prop called `key` which will be assigned a unique value. 

:oncoming_police_car: - Any Components created within a .map() must be assigned a unique key.

#### Reusable Components

Now it's time to see this in action.

In **App** comment out `<Card1 />` and `<Card2 />` as we will now replace those Components with the Components returned via the **.map()**.

```js
<section className='cards'>
	{cards}
	{/* 
		<Card1 title="Santorini" />
    		<Card2 /> 
	*/}
</section>
```


#### The Key Prop

As you may recall it was mentioned earlier that the elements would render fine however React would present a warning. 

<img src="https://i.imgur.com/Ofg12N1.png" >

This can easily be fixed by assigning a `key` prop to each element with a unique value. Since each element in an array is assigned a unique index value we will opt to use that.

```js
const cards = cardsArr.map((card, index) => {
	return (
		<Card1
			img={card.img}
			title={card.title}
			text={card.text}
			url={card.url}
			key={index}
		/>
	);
});
```

#### Passing Props To CardBody

With our Cards being rendered we first need to update `Card1` to pass the data down it's received to it's corresponding children. 

We will start with **CardBody** Component for now. 

```js
const Card1 = (props) => {
	console.log('this is props:', props);
	return (
		<div className='card' style={{ width: '18rem' }}>
			<CardImage />
			<CardBody 
              title={props.title} 
              text={props.text} 
           />
		</div>
	);
};
```

#### Updating CardBody To Use Props

Let's update `CardBody` to make use of the props.

```js
const CardBody = (props) => {
	return (
		<div className='card-body'>
			<h5 className='card-title'>{props.title}</h5>
			<p className='card-text'>{props.text}</p>
			<Button />
		</div>
	);
};
```

#### Renaming Card1 To Card

It makes more sense to rename `Card1.js` to `Card.js` and update both the import statement and the Component name in the map.

Below includes those 2 updates.

<img src="https://i.imgur.com/SLtYu9d.png">


The only task left is to pass the data to **CardImage** and **Button**. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min - Your Turn

Take a moment to update the codebase so that the **img** and **url** values are passed to the following Components:

- CardImage
- Button

Keep in the mind the following:

- Card will need to first pass those values down as props within the map
- The child Components need to include a `props` parameter 
- Any JS rendered in JSX must be wrapped in {}

:thumbsup: Click on the thumbs up when your done.

<hr>

### Final React Architecture

As we have made some design changes let's take a look at our final React Architecture design that takes into account all Components and the props being passed.

<img src="https://i.imgur.com/WlfxS7X.png" >

The above was created using [Google Draw](https://docs.google.com/drawings/d/1pG32gpXhkLqtBR2g_SrXWVeX6sza3TAq3zpP0Sjq3QM/edit?usp=sharing)

The architecture represents all the Components and the props that are being passed from parent to child Component.  This makes it much easier to understand the flow of data in our app.

### Bonus - The ...spread Operator and Object Destructuring

Since passing props is a requirement in React there are a few shortcuts we can take.

#### Using The ...spread Operator

The first is that we can use the `...spread` operator to pass all the **key:value's** down instead of writing them out one at a time.

In `Card.js` let's replace all those hard coded props, except `key`, with the `...spread` operator.

```js
const cards = cardsArr.map((card, index) => {
	return <Card {...card} key={index} />;
});
```

#### Using Object Destructuring

The other shorthand we can use is to update the Child components to destructure the **props** object and target only those key values needed by the Component. 

**CardBody**

Let's update `CardBody` to make use of **Object Destructuring**. Here we use an object as parameter that includes all the **key names** that are being passed down.

```js
const CardBody = ({ title, text, url }) => {
	return (
		<div className='card-body'>
			<h5 className='card-title'>{title}</h5>
			<p className='card-text'>{text}</p>
			<Button url={url} />
		</div>
	);
};
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Take a moment to update the `CardImage` and `Button` Components to make use of Object Destructuring.

:thumbsup_all: Click on the thumbs up when your done.

<hr>

### Additional Bonus - A Better Folder Structure

The instructor will perform a walk through of organizing the Components into a folder structure.


### Final Solution

<!-- WITH FOLDERS -->
Here is the [Final Solution](https://codesandbox.io/s/seir-831-bootstrap-props-starter-zeuwb?file=/src/App.js:72-76) without folders

<!-- WITHOUT FOLDERS -->
Here is the [Final Solution](https://codesandbox.io/s/bootstrap-solution-seir-1207-2v48i?file=/src/App.js) with folders


<!-- [Final Solution](https://codesandbox.io/s/rctrr-8-8-20-bootstrap-solution-uyvmg?file=/src/App.js) -->
