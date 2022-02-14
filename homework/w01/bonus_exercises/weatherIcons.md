## Recreating WeatherIcons in React

In this exercise, you will practice creating reusable React Components.

Use the following [CodeSandbox Starter](https://codesandbox.io/s/rctr-8-2-21-weathericons-starter-hdngl?file=/src/App.js) code

In `src/index.html` you will find five weather elements that generate the output you are seeing now.

Perform the following to complete the lab:

**Creating The Data**
* Create a new file called `weatherData.js` that contain an array of five objects with the following properties: `img`, `conditions` and `time`.
* Populate the objects based on the values from those elements in the HTML
* Export the file and import into `App.js`

**Creating The `WeatherIcons` Component**
* Look over the HTML structure used to create the weather icons
* Create a `WeatherIcons`  Component based on the HTML structure 
* Make sure to set the Component up to accept props and update the JSX to work with those props

**Rendering The `WeatherIcons` Component**
* Import the `WeatherIcons` Component into `App`
* Loop over the weatherData array data and create a `WeatherIcons` Component for each element passed
* In the loop pass the element the props it needs for img`, `conditions` and `time`. 
* App will then render those `WeatherIcons` Components

**Bonus**
* Try creating the following additional Components:

 - WeatherIcon - contains only the img 
 - WeatherData - contains both the `conditions` and `time`

**Super Bonus**
* Try working on the [The Knot](https://codesandbox.io/s/theknot-starter-ye150) exercise

**Submitting Homework**
* Add a link to your CodeSandbox [here](https://docs.google.com/spreadsheets/d/1znSaQg63lTMiBTZCmFox-6ahVYti0gU_3LQ6V3vVpFo/edit#gid=566709901)