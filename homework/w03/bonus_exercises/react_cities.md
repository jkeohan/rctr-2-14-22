# Intro To State Exercise

So far you've learned the following about React:

- Creating and nesting Components
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. At a high level you will do the following:

> Using only a single App Component you will implement the logic that allows a user to click on one of 4 small images and then update the DOM to display that image as the large image.

<img src="https://i.imgur.com/M3xQbYR.jpg" width=200/>

## Working Version
Here is a [working version](https://klk6l.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 


## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/react-cities-starter-0q48s?file=/src/App.js)


## Instructions
For this exercise you will do the following:

#### App Component
- Examine the working live solution and determine the functionality needed
- Examine the HTML provided in `src/index.html` as this contains the HTML elements needed for the design
- The data for all images is already included in the imageData.js file
- Using Array.map() loop over the data to create the small images based on the structure you decided
- Render the array of elements 
- Import `useState` into App
- Use one or more instances of `useState` to implement the logic
- Work out the remaining logic needed to implement the design

**Note:** All functionality must be placed within App and no additional Components should be created. 

### Bonus #1 - Big Image Component

- Create a new `BigImage` Component that will render the large image
- Pass the `BigImage` Component the image url it needs based the state of the application


### Bonus #2 - Additional State

- Add more state and/or update existing state in order to keep track of which small image was clicked
- Place a green border around the image to indicate that it is the image being displayed.
- Any other previously active image will have it's border color removed

