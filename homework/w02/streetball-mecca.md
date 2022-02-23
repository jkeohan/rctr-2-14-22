# Streetball Mecca

**Title:** Intro to Props<br>
**Duration:** 1-3hrs <br>
**Creator:**  Joe Keohan<br>

<hr>

So far you've learned the following about React:

- Creating and nesting Components
- Iteraring over an array and creating many instances of the same Component
- Passing props to child Component and using them in JSX

Now it's time to put it all together and do the following:

- Examine the provided React architecture
- Examine the HTML in the solution code
- Reproduce the design in the React architecture and solution code

## Working Version

Here is a [working version](https://b6gp4.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement.

Examine the working version of the app so you can see what element will be rendered as the actual card.  

## Starter Code

Here is the [Starter CodeSandbox](https://codesandbox.io/s/streetball-mecca-seir-starter-trpid).  

## Instructions

For this exercise you will do the following:

#### Folder Structure

The folder structure has already been created to help get you a head start.  All the CSS has already been included for each Component and all ID and Class names can be referenced in the working solution.

<img src="https://i.imgur.com/nkkhlBi.png" width=500>

#### Examine the React architecture

Here is the React architecture and represents how the components will be rendered and the parent > child relationship.

<img src="https://i.imgur.com/UI4GMwm.png" width=500>

#### Examine the Park Object

Each object in the `parkData.js` file contains the following key:value pairs.

```js
  {
    "code": "BK50",
    "name": "100% Playground",
    "borough": "Brooklyn",
    "boroughColor": "#306A9C",
    "overall": "56",
    "url": "https://i.imgur.com/Lf9pHxU.jpg",
    "lon": "-73.899117",
    "lat": "40.646201",
    "rating": "Mediocre",
    "color": "rgba(255,190,122,1)",
    "active": false
  }
  ```

#### App Component

- Import the `parkdata.js` file
- Pass the entire array to the `Parks` Component
- Pass the first element in the array to the `ParkImage` Component

#### Parks Component

- Create a `Parks` Component that accepts props
- It should render a `<ul>` that renders `Park` Components
- Examine the working solution and determine what HTML element is being used to render as the ul that renders the parks
- Loop over the props data passed and create a `Park` Component for each element in the array

#### Park Component

- Create a `Park` Component that accepts props
- Examine the working solution and determine what HTML element(s) being used to render LI's that compose the `Park` Component
- Assign the element with a class of `rating` the border color assigned to the elements `color` key.

#### Bonus#1

- In the `App` Component, sort the `parkData` in descending order before passing it to the `Parks` Component

#### Bonus#1
- Try Creating and Adding a **Filters Component** according to this [final working solution](https://nt8se.csb.app/). 
