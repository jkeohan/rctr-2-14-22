Title: React Floor Plan<br>
Duration: 1hr+ <br>
Creator:  Joe Keohan<br>

---


## Learning Goals

So far, you've seen the following React basics:

* How to create and render Functional Components
* How to return a function component's UI defined using JSX
* The rules and best practices of creating Components and JSX

And that's what we'll practice in this assignment!

---

# React Floor Plan

## Minimum Requirements

1. Use `CodeSandbox` to generate a new React app, titled `react-floorplan`.  

1. Define the following components and code them such that they fulfill their responsibilities:

	| Component | Responsibilities |
	|---|---|
	| `<FloorPlan>` | Rendered by `<App>`<br>Renders the following components:<br>- A `<Kitchen>` component<br>- A `<LivingRoom>` component<br>- Three `<Bedroom>` components<br>- Two `<Bath>` components<br>**Render the components in any order you wish to make the floor plan more interesting** |
	| `<Kitchen>` | Renders the text "Kitchen" and the following components:<br>- A `<Oven>` component<br>- A `<Sink>` component |
	| `<LivingRoom>` | Renders the text "Living Room" |
	| `<Bedroom1>` | Renders the text "Bedroom 1"|
    | `<Bedroom2>` | Renders the text "Bedroom 2"|
    | `<Bedroom3>` | Renders the text "Bedroom 3"|
	| `<FullBath>` | Renders the text "Full Bath"" |
    | `<HalfBath>` | Renders the text "Half Bath" |
	| `<Oven>` | Renders the text "Oven" |
	| `<Sink>` | Renders the text "Sink" |

1. Define each component in its own file. The naming convention to use for a component's file is UpperCamelCase, for example, a `<SomeComponent>` component's file would be named `SomeComponent.js`

1. Export each component from its module. For example:

	```js
	import React from 'react';
	
	function SomeComponent(props) {
	  return (
	    <div>
	      <h1>SomeComponent</h1>
	    </div>
	  );
	}
	
	export default SomeComponent;
	```

1. Add the following CSS inside of **index.css** to style each component's wrapping `<div>` to make it easier to visualize the components:

```css
div {
  border: 1px solid grey;
  margin: 5px;
  padding: 5px;
}
```

With the minimum requirements complete, the output should resemble:

<img src="https://i.imgur.com/g0T8RNK.png" width=500/>


## Bonus

Style the components to make the output look like this [solution](https://z3qii.csb.app/).



<img src="https://i.imgur.com/NhRcNrk.png" width=500>

### Hints

* Use `className` and/or `id` on React Elements (`<div>`, `<p>`, `<span>`, etc.) to apply CSS styling using CSS rules in the **index.css** file.
* Styling the `<FloorPlan>` component as a CSS Grid is a great way to layout its children (grid items).


---
