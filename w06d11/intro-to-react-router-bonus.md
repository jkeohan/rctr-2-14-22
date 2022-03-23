# React Router

<img src="https://i.imgur.com/UcmwbaK.png" width=300/>

## Learning Objectives

### React Bitcoin Currency

Here is what we are looking to build:  [Bitcoin Solution Code](https://efzzl.csb.app/)

Here is our [Starter Code](https://codesandbox.io/s/rctr-router-p2-bitcoin-starter-wznck?file=/src/components/App/App.js)

<!-- Here is our [Starter Code](https://codesandbox.io/s/rctr-router-p2-bitcoin-starter-8e2vp?file=/src/components/App/App.js) -->

<!-- Here is our [Starter Code](https://codesandbox.io/s/bitcoin-starter-8-2-21-iidrbs) -->



## Currencies Route

If we look at this component we see a long list of currencies. 

<img src="https://i.imgur.com/D57VJ1G.png" />

## Currencies Component

This component renders the individual currencies.

What happens if we click on a link? It works, but the whole page reloads which is a poor choice of UI. 

Lets go ahead and replace the `a` tag with a `<Link>` component. 

```jsx
// src/Components/Currencies/Currencies.js
import { Link } from 'react-router-dom'

  let list = listOfCurrencies.map(item => {
      return (
        <div className="currency" key={item.currency}>
           <p>
            <Link to={"/currencies/" + item.currency}>{item.currency}</Link>:{" "}
            {item.country}
          </p>
        </div>
      );
    });

  render() {
      return <div>{list}</div>;
  }

```

Great! Now go back to the page and click the link again, what happens?

It changes the route for us (notice the URL changing) but we don't have any
routes set up to match that url so it `Redirects` us back to the home page. 


### Currency Component 

If we take a moment to examine the `Currency` Component we will see that there is the following variable with the url to the `conidesk` api.

```js
const coindeskURL = "https://api.coindesk.com/v1/bpi/currentprice/";
```

If we try going to the above url we will see the following:

<img src="https://i.imgur.com/v1C3VSS.png"/>


If we append a bitcoin currency we should see that the url does return that currencies data. 

```js
https://api.coindesk.com/v1/bpi/currentprice/AFN
```

<img src="https://i.imgur.com/ADE1k6U.png" width=400/>

This is the data we will use to render the info dynamically for the currency each time the user clicks to see a currency. 

### Currency Route

In order to active this route we need  add another `<Route>` component in `App`. 

This time though we want to include a `parameter`.

Clicking on a currency will now update our URL to the following:

```js
https://vthmi.csb.app/currencies/AFN
```

It seems as though the info we need to make the API call is already in the route. We can use that as part of our routing logic. 

**App.js**

In **App.js** Let's create a new route that includes a `url parameter`. This is done by appending a `:paramName` after the path.

```html
  <main>
    <Route exact path="/" component={Home} />
    <Route path="/currencies/:currency" component={Currency} />
    <Route path="/currencies" component={Currencies} />
    <Redirect to="/" />
  </main>
  ```

Clicking on a specific currency should display the following, which includes both the **Currency** component as well as the **Currencies** component. 

<img src="https://i.imgur.com/rHQRdII.png" width=400/>

<hr>

:question: How can we update the route to display only the **Currencies** route and not both the **Currencies** and **Currency** routes? 

<hr>

Of course the answer is to add the exact keyword to both routes. 
```js
  <main>
    <Route exact path="/" component={Home} />
    <Route exact path="/currencies/:currency" component={Currency} />
    <Route exact path="/currencies" component={Currencies} />
    <Redirect to="/" />
  </main>
```

#### Router Props "match"

If we examine the `Currency` Component in React DevTools we should see the following: 

<img src="https://i.imgur.com/EVfxNzn.png" width=500/>

So it looks like `props.match.params.currency` contains the currency code that we need to make the API call. 

## Adding useState and useEffect to Currency Component

Knowing that in order to view the most active price we will need to make an API call.  Once the data has been fetched we will need to update state in order to force the component to re-render. 

In order to implement this logic we will need to make use of both `useState` and `useEffect`, so let's import them into the `Currency` Component

```js
import React, {useState, useEffect} from "react";
```

Let's setup our state. 

```js
const [currency, setCurrency] = useState(null);
```

The Currency component will be responsible for making the API call to `coindesk` to retrieve the current price of the currency. 

We will make the call when the component first mounts, `componentDidMount`,  and will do so within `useEffect`. 


```js
  useEffect(() => {
    const makeApiCall = async () => {
      const currency = props.match.params.currency;
      const url = `${coindeskURL}${currency}.json`
      const res  =  await fetch(url)
      const json = await res.json()
      let currencyPrice = json.bpi[currency].rate;
      setCurrency(currencyPrice)
    }
    makeApiCall()
  },[])
```

The last edits required are to update the JSX to include the required info.  

```html
<h1>Bitcoin price in {props.match.params.currency}</h1>
<div className="price">Price: {currency}</div>
```

## New Feature Request

The client has just asked that we now include a new feature.  They would like to display the currency name in the header.  The header will look like this when no currency is selected: 

<img src="https://i.imgur.com/guMrAJb.png" width=500/>

And then update to include the currency name when a currency is active.

<img src="https://i.imgur.com/ukBuPSI.png" width=500/>

First take a look at `App` to at least add the `>` to the existing JSX.

```html
<Link to="/currencies">Currencies ></Link>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

Based on your current knowledge of React and React Router, think of a way to implement this logic.  

- Take 2 minutes to think how you would implement this request
- The instructor will ask you to post your answers in a slack thread


<hr>

## Lifting State

**App.js**

In order to show the currency value in `App` we need to pass, or better yet lift, the currency name from `Currency` to `App`.  

In order to to this we need to pass down a function that will call `setCurrency`.  So let's create a new function to pass down.


```js
  const handleClick = price => {
    setCurrency(price);
  };
```

Here is the thing though.  The way our route is configured we can't pass down props. 

```html
 <Route path="/currencies/:currency" component={Currency}/>
```

In order to do so we will need to replace `component` with the `render` method in the route and pass down the routerProps.

```html
<Route path="/currencies/:currency" render={ () => <Currency setCurrency={setCurrency}/>} />
```

Let's see if that works.  

Hmmmm...it looks like we broke it. 



<img src="https://i.imgur.com/YWH8A81.png" width=400/>

Let's comment out the **makeApiCall()** function in the **useEffect** in the `Currency` component and then take a look at the `Currency` Component in DevTool. 

```js
useffect(() => {
  // code...
  // makeApiCall()
})

// AND IN THE JSX
  {/* <h1>Bitcoin price in {props.match.params.currency}</h1> */}
```

It seems as though we have lost all of the previous router props that we had access to just moments before. 

<img src="https://i.imgur.com/FGMRfVo.png" width=500/>

The render method requires that we pass the router props to the callback function.  We can then manually assign the props. 

```js
<Route path="/currencies/:currency" render={(routerProps) => 
  <Currency
    history={ routerProps.history}
    location={ routerProps.location }
    match={ routerProps.match }
  >
} />
```

Or a much better way would be to pass them all down using the `...spread` operator. 

> The `...` (spread operator) is allowing us to "destructure" the props object
> being passed by `Router` and apply each of its key/value pairs as props on the
> `Currency` component.


```js
<Route path="/currencies/:currency" render={(routerProps) => 
  <Currency 
    {...routerProps}
  />} 
/>
```

Let's also pass down the `setCurrency` function so that we can lift state. 
```js
<Route path="/currencies/:currency" render={(routerProps) => 
  <Currency 
    setCurrency={setCurrency}
    {...routerProps}
  />} 
/>
```

Confirm in DevTools that those props are back and uncomment out the code. 


In the `Currency` Component we need to call `props.setCurrency(currency)` in the `makeApiCall` function. 

```js
props.setCurrency(currency)
```

### Update Navigation

Let's update App to include the currency name in the navigation by adding the following:

```js
<Link to="/currencies">{
      currency ? `Currencies List > ${currency}` : 
      `Currencies List > `
  }</Link>
```

### Clear Previous Value
If we click the links a few times we will see that our new feature doesn't yet clear the previous value when we are on `/currencies` or the `/` home route.  

For that we need to add an `onClick` event to both of those `Link`'s

```html
<Link onClick={() => setCurrency('')}to="/">
  <img
    src="https://en.bitcoin.it/w/images/en/2/29/BC_Logo_.png"
    alt=""
  />
  <h1>Bitcoin prices</h1>
</Link>
<Link onClick={() => setCurrency('')} to="/currencies">
  {currency ? `Currencies List > ${currency}` : `Currencies List`}
</Link>
```

Now uncomment out the code in `Currency` Component and we should be good to go.  

<!-- We still have some weird issue where both the `currencies` and `currencies/:currency` routes display at the same time. 

<img src="https://i.imgur.com/3EQxfuL.png" width=300/>



 Let's make use of a new React Router Component called `Switch` that will help fix this.   -->

## Using Switch 

Switch works just like the switch/case statements in javascript. We're comparing
string values (in this case, routes) and executing conditions (rendering
components) based on what matches turn out true.

Since we're not using switch right now the two components are stacked on top of each other! The Home and the
Currencies component. That's silly.

> Why does this happen?

There are two ways to handle this: using the Switch component, or specifying
`exact` on routes.

Let's update our routes in `App.js` once last time to replace `exact` with the `Switch` component. 

Lets first import Switch

```js
import { Route, Link, Switch } from 'react-router-dom'
```

And then use the Switch component. 

```html
        <Switch>
          <Route path="/"component={Home} />
          <Route path="/currencies/:currency"
            render={(routerProps) => <Currency setCurrency={setCurrency} {...routerProps} /> }
          />
          <Route path="/currencies" component={Currencies}
          />
        </Switch>
```

Does this work as expected? 

Try putting `exact` on the `/` path route component.

```js
<Route exact path="/" component={Home} />
```

<!-- Beautiful! this is a great solution, unless we have many different routes.

If we had a list of routes like:

- `/currencies`
- `/currencies/new`
- `/currencies/:id` etc

we would have to put `exact` on `/currencies` or else, any time we went to
`/currencies/something` it would match both the root (`/currencies`) AND the
`/currencies/something` routes and both would be rendered.

We can avoid all this by just using `<Switch />`.

Back in `App.js`, let's import the `<Switch />` component and then wrap all of
our routes in it. -->

<!-- ```html
import { Route, Link, Switch } from 'react-router-dom'

  return(
    <div>
      <nav>
        <Link to="/">
          <img src="https://en.bitcoin.it/w/images/en/2/29/BC_Logo_.png" alt=""/>
          <h1>Bitcoin prices</h1>
        </Link>
        <Link to="/currencies">Currency List</Link>
      </nav>
      <main>
        <Switch>
          <Route exact path="/"component={Home} />
          <Route path="/currencies/:currency"
            render={(routerProps) => <Currency setCurrency={setCurrency} {...routerProps} /> }
          />
          <Route path="/currencies" component={Currencies}
          />
        </Switch>
      </main>
    </div>
  )
``` -->

## Redirects Revisited

Redirects using react router are incredibly easy. `Redirect` is just another
component we can import and use by passing it a few props.

Let's add another Redirect to account for users who manually type in `currency` instead of `currencies`

```js
<Route path="/currency" render={() => <Redirect to="/currencies" />} />
```

Redirect only requires a `to` prop which tells it what path to redirect to.

Here is the [Solution Code](https://codesandbox.io/s/bitcoin-router-solution-with-history-0kpm9)

## Bonus - Working With `History` 

We can make use of the the `history.push` method to push routes into the browsers url.

In the `Currency` Component let's create a button that when called will navigate the user back to the `currencies` route.

Let's add a button and assign it the `handleCLick` function. 

```js
 <button onClick={props.history.push('/')}> Home</button>
```
