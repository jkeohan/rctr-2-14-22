# Traffic Light

Objectives:

- Creating and nest Components
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component

## Working Version

Here is a <a target="_" href="https://zhtbi.csb.app/">working CodeSandBox solution</a> of the app so you can examine the components in React DevTools.

## Starter CodeSandbox

Here is our <a target="_" href="https://codesandbox.io/s/traffic-light-single-app-component-starter-pqrpw">Starter CodeSandbox</a>

### Instructions


#### TrafficLight Component

- Examine the working live solution and determine the functionality needed
- Examine the HTML in `App.js` as this contains the HTML elements needed for the design 
- All the CSS has been included in `styles.css`
- The `bulbData.js` file contains the data 
  
<details><summary>bulbData.js</summary>

```javascript
export default [
  {id: 'stop', name:'Stop', color: 'red'},
  {id: 'slow', name: 'Slow', color: 'yellow'},
  {id: 'go', name: 'Go', color: 'green'},
]
```
</details>

- Create a `TrafficLight` Component which will be used to render all 3 traffic lights
- It will receive a prop called `color` and render the color using a style tag: **style={{ background: props.color }}**
- Keep in mind that all 3 Components will be passed black as this is the starting color for each `Trafficlight`

#### App Component

- Import `bulbData.js` and set it 
- Import `useState` into `App` as follows: **const [activeBulb, setActiveBulb] = useState({})**
- Import the `TrafficLight` Component
- Loop over the bulbData and return a `TrafficLight` Component and pass each the color it needs
- Create a `handleControls` function that will be passed the object of which button was clicked which it will use to update state.
- Loop over the bulbData again and return the html based on the existing design.  Also make sure to assign an `onClick` event that is passed the object. 

### Bonus - Bulb Component

- Create a new `Bulb` Component that will render the a single bulb
- Pass the `Bulb` Component the color it needs based the state of the application
  
