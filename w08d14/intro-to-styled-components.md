[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# React Styling

## Learning Objectives

- Compare and contrast several ways to implement styling in React

- Use **Styled Components** API to create components

## Framing

As with all things `coding` there are many ways to accomplish the same thing. Take for instance the need to run simple conditional logic. Depending on the use case any of the follow might suffice:

- if/else
- switch statement
- ternary operators

What about looping and/or filtering a set of data. Once again depending on the use case several approaches could be taken:

- for loop
- for of loop (Array specific)
- for in loop (Object specific)
- while
- Array.forEach()

Every React app will require styling and depending on your needs and/or level of experience several approaches can be taken:

- CSS Preprocessors such as Sass or Less
- CSS Frameworks such as React-Strap or Materialize
- CSS in JS such as Styled Components
- CSS Architecture such as BEm or CSS Modules

<!-- - a single CSS file for the entire app
- individual CSS files for each Component
- inline styles and/or JS conditional logic to update values
- using CSS preprocessors such as Sass/SCSS or Less
- importing a library such as Styled Components -->

Here is a subsesction of **Styling** as per the [2021 React Developers Roadmap](https://1.bp.blogspot.com/-evyQ2_bYeT8/YAl1uSUr9oI/AAAAAAAAl0o/eRsyUSaBLP8Rv7BKokqDIAYyr92SOyNzwCLcBGAsYHQ/s2048/The%2BReact%2BRoadMap%2Bfor%2BWeb%2BDevelopers.png)

<img src="https://i.imgur.com/N1o3TCM.png">
<!-- 
<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Before we go on let's take a moment to answer the following question:

:question: How would you define what a Component is and what you would consider when creating them?

<hr> -->

<!-- ## Components As Self-Contained

Based on the answers provided to the previous question it's clear that the first concept we need to keep in mind is that `Components` are meant to be **self-contained** and **reusable**.

<hr> -->

## Components As Self-Contained


<!-- #### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min -->

Components, React or otherwise, are now becoming the standard for sharing small pieces of functionality.

Let's take a look at a few different Component libraries:

- [https://bit.dev/](https://bit.dev/)
- [Reactstrap](https://reactstrap.github.io/?path=/story/home-installation--page)
- [Shopify Polaris](https://polaris.shopify.com/components/get-started#navigation)

There is also another powerful site called [StoryBook](https://storybook.js.org/) that enables developers to create and share Components.

<!-- <hr> -->
<!-- 
Since Components should be built as self contained and reusable entities it makes sense they would be constructed with all the internal logic needed to control their behavior.

We can use values in `props` and `state` to thoroughly control the view, including styling.

Fortunately, lots of techniques, frameworks, tooling and other open source projects have been built and popularized to fill these gaps. Three popular ways that you'll likely encounter are:

- CSS Stylesheets
- Inline Styles
- CSS-in-JS (CSS Modules & Styled Components) -->

## Starter Code

Here is the [Starter Code](https://codesandbox.io/s/styles-4-ways-starter-13qy5?file=/src/App.js) we will be using for this lecture.

## CSS Stylesheet

The first and most basic approach is importing CSS files directly into our components.

```js
import './styles.css';
```

We can import a single `css` file at the highest level in the app or create separate `css` files that target a specific Component. A great way to organize your app would be to place `Components` into separate folders along with the `css` file.

<img src="https://i.imgur.com/8WUzfcr.png" />

#### Benefits

- Anyone working in front end design knows how to use them
- Smaller subset of css files making it easy to find and edit
- Full access to all CSS specifications (animations, pseudo-classes, pseudo-elements, etc.)

#### Drawbacks

- CSS may be overridden by more specific rules

## Inline Styling

The term `separation of concerns` is a design principle that refers to separating functionality into distinct sections to make it modular. Under `SoC`, it's logical that we separate our CSS, HTML and JS into independent files which has been the standard in the web dev community since it's birth.

As a result, [inline styles were considered bad practice](https://stackoverflow.com/questions/2612483/whats-so-bad-about-in-line-css).

Inline styles, particularly in the context of components, does make a lot of sense though and aligns with the idea that `what goes together should stay together`.

### Style Object

<!-- When using `inline-styles` we might opt to assign the style directly in the JSX.

```html
<button style={{
    backgroundColor: primary,
    color: '#fff',
    padding: '7px 14px',
    margin: '0 5px',
    borderRadius: '5px',
    border: '1px solid transparent',
    }}>Primary</button>
``` -->

When using `inline-styles` we might create a **styles** object that includes the default styles for all buttons and assign those styles directly.

```js
export default function InlineStyle() {
  const buttonStyles = {
    color: '#fff',
    padding: '7px 14px',
    margin: '0 5px',
    borderRadius: '5px',
    border: '1px solid transparent',
  };


 <button style={buttonStyles}>Primary</button>
```

We could also use another object that defines styles for a specific button but yet inherits all the previous button styles.

```js
const primaryStyles = {
  ...buttonStyles,
  backgroundColor: primary,
};

return (
  <div>
    <h2>Inline Styles</h2>
    <button style={primaryStyles}>Primary</button>
    <button>Secondary</button>
  </div>
);
```

#### Conditional Logic

We can also used conditional logic to determine which values should be assigned to specific css rules.

```js
const buttonStyles = {
  backgroundColor: props.primary ? primary : danger,
  // ...rest of styles
};
```

This works well enough for the most basic logic of a single button. But when multiple buttons are introduced that require different background colors and/or effects such as `hover`, then the code can get messy very quickly.

#### Benefits of Styled Objects

- No special tools needed and takes advantage of basic JS and CSS
- Leverage `props` and `state` to make dynamic updates
- Component level styles stay with the component

#### Drawbacks of Styled Objects

- Limited support of CSS specification (no animations, pseudo-classes, pseudo-elements, etc.)
- Hard to read and difficult to override (must use !important flag)
- Hard to document and maintain

## CSS in JS

CSS in JS lets you you style your Components with JavaScript instead of CSS. Then, when your application is run, the JavaScript is parsed and generates CSS, which is attached to your DOM directly.

### CSS Modules

One major issues of standard CSS or Sass/SCSS is that there is no concept of true encapsulation and requires that the developer define each and every unique class name.

`CSS modules` however create dynamic class names for each locally defined style thereby making sure classnames didn't conflict.

It's creators designed it to be lightweight and so it only support a handful of features.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at a site like [Buffer](https://buffer.com/) which uses CSS Modules.

We will focus our attention specifically on the `header` element of their home page and the class names.

<img src="https://i.imgur.com/W19mc86.png" width=500/>

<hr>

The basic premise is that the css classes are converted using a preprocessor into unique names in order to create `local scoping`.

While additional tooling is needed to handle the processing of the files, `create-react-app`, which `CodeSandox` uses, includes this tooling by default.

The actual css file must include `.module` in it's name. So if you are using standard css then the name might be `styles.module.css` but if your using SCSS then it would be `styles.module.scss`.

<img src="https://i.imgur.com/FWdD5YU.png" />

#### Importing styles

The file is then imported, but this time we store the import in a variable as it returns an object.

Let's also add a console log and see what that import looks like.

```js
import styles from './styles.module.css';
console.log('styles', styles);
```

From the console log it's clear that the css rules are assigned as keys and the values are `module` specific.

<img src="https://i.imgur.com/xQOPP0d.png" />

The rules are then applied to the elements using dot notation.

```html
<div className="{styles.container}">
  <h2>Modules</h2>
  <button className="{styles.button}">Primary</button>
  <button>Secondary</button>
</div>
```

If we take a look at the `button` element in the `Elements` Tab in DevTools we will see the following:

<img src="https://i.imgur.com/kDWUghQ.png" />

Since this isn't a standard CSS name there is no way these styles will conflict with another element in the global scope that has been assigned a class of `.button` as well.

#### Adding Another Class

If we want to add the **primary** class as well to the button then we will need to write it as follows:

```html
<button className="{`${styles.button} ${styles.primary}`}>Primary</button>
```

#### Benefits of CSS Modules

- Component level styles stay with the component
- Import/Export common styles between files
- Access to full CSS specification including support of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) for variable support

#### Drawbacks of CSS Modules

- Limited access to `props` and `state`
- No Sass/SCSS like features except `composes`

## Styled Components

One of the most popular and advanced CSS-in-JS libraries is [Styled Components](https://www.styled-components.com/).

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now that were jumping into styled components let's take a look at a [CoinMarketCap](https://coinmarketcap.com/) and see styled components in action. If React Developer Tools if we highlight the navigation we can reference to **sytled.div**.

<!-- <img src="https://i.imgur.com/NW34yw7.png"> -->

<img src="https://i.imgur.com/gRJObWz.png">
<!-- vimeo -->
<!-- <img src="https://i.imgur.com/OfpsvWR.png" width=500/> -->

<hr>

**Install Styled Components**

Since `styled components` in a third party library it must first be installed as an NPM package.

<img src="https://i.imgur.com/zCX1cFF.png" />

<br>

**Import The Library**

Which then must be imported.

```js
import styled from 'styled-components';
```

<!-- Styled Components are created ES6 feature called a `Tagged Template Literal`, or perhaps you know it as `String Template Literal`. -->

**Using Styled Components**

Let's create two styled components, one for the **div** and the other for the `button`.

```js
const Container = styled.div``;

const PrimaryButton = styled.button``;
```

**Adding Styles**

Let's add some styles to the `Container`. Adding a `color` can be done by either written literally by it's name/hex/rgb or by referencing a variable.

```js
const Container = styled.div`
  color: ${warning};
`;
```

Now the `Button`.

```js
const PrimaryButton = styled.button`
  background-color: ${primary};
`;
```

Let's make use of the new styled components.

```html
<Container>
  <h2>Styled Components</h2>
  <PrimaryButton>Primary</PrimaryButton>
  <button>Secondary</button>
</Container>
```

If we take a look at those elements in the `Elements` Tab of DevTools we will see that the class names begin with `sc-` and then end with a mix of difference characters.

<img src="https://i.imgur.com/QYiiYxc.png" />

Let's also take a look in React Dev Tools.

<img src="https://i.imgur.com/96JeTdo.png">

**Common CSS**

Let's take a look at `css` and use it to create and share css between multiple components.

The functions need to be imported.

```js
import styled, { css } from 'styled-components';
```

Then we create our shared styles.

```js
const sharedStyles = css`
  color: #fff;
  padding: 7px 14px;
  margin: 0 5px;
  border-radius: 5px;
  border: 1px solid transparent;
`;
```

And include this in the styled components that need it.

```js
const PrimaryButton = styled.button`
  ${(props) => sharedStyles};
  background-color: ${primary};
`;
```

#### Adding Hover

Let's also add a `hover` effect as well. Styled Components make use of Sass/SCSS syntax and since `hover` is a `pseudoclass` so we must include `&:hover`.

```js
const PrimaryButton = styled.button`
  ${(props) => sharedStyles};
  background-color: ${primary};
  &:hover {
    background-color: red;
  }
`;
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Create a **SecondaryButton** Styled Component

<hr>

### Conditional Logic

Just as we did with inline styles we can use conditional logic to determine which css values are assigned to a style.

Conditional logic can be added in the following ways:

- a single ternary operator
- a callback function based on `prop` passed directly to the styled component

#### Ternary Operator

Let's try and set the `border-radius` based on a prop value passed from the parent.

Being that were using `string template literals` when creating the component we must include `${}` when referencing variables.

```js
const PrimaryButton = styled.button`
  border-radius: ${props.primary ? '5px' : '20px'};
`;
```

Here is what the rendered Components look like in React DevTools.  It's clear that there is no prop of **primary** being passed down, however there is the following prop: **children: "Primary"**. 


<img src="https://i.imgur.com/3Bn8TWF.png" width=300/>

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Refactor the route in App.js to pass down a prop of **primary={true}**

**Note:** You will have to refactor the route to make use of the **render** method instead of **component**

<hr>

### Passing Styled Components Their Own Props

First take a moment to remove the **primary prop** being passed from App

Besides accepting props from the parent directly we can also pass a `styled component` unique props of it's own just as we would do with any Component.

```js
<PrimaryButton primary>Primary</PrimaryButton>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

:question: Since we only passed a prop name but no value use DevTools to explore if it's been assigned a value and what that value might be.

<hr>

So it appears it doesn't actually need to be assigned a value and will assign a value of `true` just because the prop exists.

Now within the `styled component` we can't just reference the prop that is being passed directly to the component like before but now need to pass that value via an `anonymous function` and run additional JS conditional logic.

```js
border-radius: ${props => {
    console.log('props', props)
    if (props.primary) return '20px'
    return '0'
}};
```

Note: This props is not the same as the props being passed down from the parent.

Here is what the console log looks like

<img src="https://i.imgur.com/JvgqV1F.png" />

And then we can either use it directly as assigned or run conditional logic.

```js
border-radius: ${props => {
    console.log('props', props)
    return (props.primary) ? '20px' : '0'
}};
```

We do have the option to also pass the prop a value as well.

```js
<ButtonTwo primary={false}>Customized</ButtonTwo>
```

### Helpers

Styled components come with several additional [Helper functions](https://styled-components.com/docs/api#helpers). We've taken a look at **css** so now lets take a look at **keyframes**

<!-- **CSS**

Let's take a look at `css` and use it to create and share css between multiple components.

The functions need to be imported.

```js
import styled, { css } from 'styled-components';
```

Then we create our shared styles.

```js
const sharedStyles = css`
	color: ${(props) => (props.standard ? white : warning)};
`;
```

And include this in the styled components that need it.

```js
const Button = styled.button`
	${(props) => sharedStyles}
  //...rest of css
`;
``` -->

<!-- **KeyFrames**

The functions need to be imported.

```js
import styled, { css, keyframes } from 'styled-components';
```

Then create a new keyframe and add the desired animation and timing.

```
const fadeIn = keyframes`
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
`
```

Incorporate the keyframe into the styled component.

```js
const Button = styled.button`
	${(props) => sharedStyles}
	animation: 1s ${fadeIn} ease-out;
	//...rest of css
`;
```

**Conditional Rendering**

We can also conditionally render the animation on a per component basis based the props passed to it directly. This involves a combination of `css` and `keyframes`.

First let's assign a new prop value to the Primary button in order to indicate that this is the only button that should animate.

```html
<PrimaryButton primary animate>Primary</PrimaryButton>
```

Let's refactor the current animation value into a fat arrow and run the conditional logic there:

```js
animation: ${(props) =>
  props.animate ? css`${fadeIn} 1s ease-out;`: ''
};
```

This should do the trick but we can also opt to place the css code into it's own external function.

```js
const animate = (props) =>
	props.animate
		? css`
				${fadeIn} 1s ease-out;
		  `
		: '';
```

And then reference that animation.

```js
animation: ${animate};
``` -->

#### Benefits of Styled Components

- Full access to `props` and `state`
- Component level styles stay with the component
- Access to full CSS specification including support of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) for variable support
- Sass-like features (such as nesting) and much more if you add [Polished](https://polished.js.org/)

#### Drawbacks of Styled Components

- dependency required
- learning curve (much to learn)

### Solution Code

Here is the [Solution Code](https://codesandbox.io/s/styles-4-ways-starter-8-2-21-flp8j?file=/src/StyledComponents/index.js)

<!-- [6 Ways To Style](https://codesandbox.io/s/styles-6-ways-solution-wumw8?file=/src/InlineStylesWithHooks/index.js) -->

<!-- Here is the [Solution Code](https://codesandbox.io/s/styles-4-ways-starter-10-22-20-gpf9t?file=/src/StyledComponents/index.js) -->

<!-- ### Bonus - Sass/SCSS

Both Sass (Syntactically Awesome Style Sheets) and SCSS (Sassy CSS) are extensions to CSS and provide a robust set of functionality.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at the [Sass](https://sass-lang.com/guide) documentation

<hr>

[Sass Solution](https://codesandbox.io/s/styles-4-ways-solution-wumw8?file=/src/Modules/styles.module.scss) -->

### Bonus - Tailwind CSS

Tailwind CSS is a utility-first CSS framework that is used to rapidly build custom UI interfaces.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at the [Tailwind CSS](https://v2.tailwindcss.com/docs) documentation

<hr>

Here is an example of a [Portfolio Landing Page](https://codepen.io/GSometimes/pen/VwMoyPb) made with Tailwind CSS.

## Additional Resources

- [CSS Modules](https://github.com/css-modules/css-modules#composition).
- [Styled Components](https://styled-components.com/docs/faqs)
- [Building a reusable Component System with React.js and styled-components](https://levelup.gitconnected.com/building-a-reusable-component-system-with-react-js-and-styled-components-4e9f1018a31c)
- [React Styling Options](https://www.sitepoint.com/react-components-styling-options/)
