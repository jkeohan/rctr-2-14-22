# Light Levels Refactor For Redux

## Working Version
Here is a [working version](https://r73sr.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 

It does not contain `Redux`

<img src="https://i.imgur.com/yx9Z8M0.png" width=500/>

## Starter CodeSandbox

<!-- this starter code includes useReducer solution-->
<!-- Here is our [Starter CodeSandbox](https://codesandbox.io/s/light-levels-redux-starter-forked-r22cl3?file=/src/Components/App.js) -->

<!-- this starter code includes basic useState solution -->
Here is our [Starter CodeSandbox](https://codesandbox.io/s/light-levels-redux-starter-ebp97o)



## Instructions
For this exercise you will do the following:

### App Component
- Install redux packages (`react-redux & redux`)
- Add Redux to our App by importing `createStore` from `redux`
- Move the reducer and initial state to as separate file and refactor to work with Redux
- Import the reducer back into App
- Create a `store` and pass it the imported reducer
- Wrap the child components in `Provider`
- Remove any props being passed down to the child components as they will consume state value from the global store directly


#### Controls Component
- Subscribe component to the global store using `connect`
- Create a `mapStateToPropsMap` function that maps state values to their corresponding prop values
- Update the component to use any new mapping names (if needed)
- Dispatch actions

#### Light Component
- Subscribe component to the global store using `connect`
- Create a `mapStateToPropsMap` function that maps state values to their corresponding prop values
- Dispatch actions
