# Testing in React 

## Learning Objectives
* Discuss the features of Jest and Enzyme

* Implement test driven development processes
* Use Jest and Enzyme to test React applications


## Framing 

We all run **tests** with each line of code we write.  That test is **did the thing work as expected** or did it break something.  Although we can't truly escape writing our code in this fashion  there is a flaw in that approach and one we have all experienced at some point. Fixing one problem breaks something else all together. 

This is where formal testing comes in. It ensures that your app continues to function as expected, and can save you massive headaches down the road, a few of which are:

- Ensuring that the code continues to yield the desired result, and does not break with further development.
- Testing for various use cases, rather than just the one that you performed.
- Reminding you why code is written a certain way (to handle the finicky third-party package rendering, or ensure that functions come to completion in the proper order, etc.)



## Testing Libraries

We will be using the following libraries to create and run our tests.

- [Jest](https://jestjs.io/en/)
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
- [Enzyme](https://github.com/airbnb/enzyme)


**Jest** and **React Testing Library** are used very much in conjunction with one another, and it is nearly impossible to talk about one without the other. You can think of **Jest** as doing the actual testing, while **React Testing Library** recreates the thing to be tested 

**Enzyme** is used to mimic JQuery's DOM manipulation library to make testing React even easier. It allows us to grab the state of the component, simulate user actions, and grab elements from the virtual DOM.


## Starting With Jest
[Jest](https://jestjs.io/en/) is an easy to configure testing framework built by Facebook for testing JavaScript code. 

### Running A Single Test
Test are created using either the **it()** or **test()** functions and take in 2 params: 

- a message which describes the test
- callback function which contains the test

```js
test('does this thing', () => {});

// VS

it('should do this thing', () => {});
```

### Creating A Suite Of Tests
Several tests can be run against a common feature and should be combined into a **suite** of tests.  This can be done by wrapping them in **describe()** which also takes in 2 params:

- a message which describes the test block
- callback function which contains all the tests

Here is an example of several tests being run against an algo that flattens an array. 
```js
// TEST SUITE
describe('Flatten Array Tests', () => {
  // TEST CASE
  it("should flatten an array.", () => {
    // test goes here
  })
  // TEST CASE
  it("should return an empty array if the input is an empty array.", () => {
    // test goes here
  })
})
```

<!-- 
<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's take a look at the docs on running tests in [CodeSandbox](https://codesandbox.io/docs/tests)

<hr> -->

### Starter Code

<!-- The starter code we will be using is a full **create-react-app** build and is slightly different then the React app we are able to spin up using the **React CodeSandbox** template.   -->

<!-- Here is the starter code: [CodeSandbox React Testing](https://codesandbox.io/s/rctr-react-testing-7w0uk) -->
Here is the starter code: [CodeSandbox React Testing](https://codesandbox.io/s/rctr-react-testing-starter-ldlz8)

<!-- [Solution Code](https://codesandbox.io/s/rctr-react-testing-solution-up-to-counter-v1ccw?file=/src/App.js) -->

## Flatten An Array Test

Let's write our first test. Inside the **src** folder there is a folder called **algos** which contains two files: **flatten.js** and **flatten.test.js**

<img src="https://i.imgur.com/YyYVKdg.png" />


If we take a look at **flatten.js** we will see it contains the code needed to flatten an array of nested arrays.  

```js
function flatten(arr, result = []) {
  arr.forEach(elm => {
    switch(true) {
      case Array.isArray(elm) : 
        flatten(elm, result); break
      default :  
        result.push(elm);
    }
  });
  return result;
}

export default flatten;
```

This code would indeed return a flattened array. We can even test this out in this [repl](https://repl.it/@jkeohan/algo-flatten-array-2-solutions). 


```js
flatten([1,[2,3],[[4],5]]) => [1,2,3,4,5]
```



### Our First Test

If we take a look at **flatten.test.js** we see that contains no code and since there are no tests to run our testing results should be empty. 

<img src="https://i.imgur.com/lKclmfd.png" />

<!-- Of course the idea here is that the user would need to work out the logic to solve the algo themselves and then run the tests to validate they got it right.  -->

Our goal is to create a series of tests that will validate the results of running that code.  

Let's start by creating a single test that includes the **input** and **output** we expect.

```js
it("should flatten an array of arrays", () => {
  // input
  const nestedArray = [1,[2,3],[[4],5]];
  // output
  const flatArray = [1, 2, 3, 4, 5];
});
```

We now need to validate that if **flatten()** received **nestedArray** as input that its output would be **flatArray**.  

In order to do that we will use the [expect()](https://jestjs.io/docs/expect) function which gives us access to a number of custom **matchers**, one of which is **.toEqual**. 

```js
it("should flatten an array of arrays", () => {
   // input
  const nestedArray = [1,[2,3],[[4],5]];
  // output
  const flatArray = [1, 2, 3, 4, 5];
  expect(flatten(nestedArray)).toEqual(flatArray);
});
```

Since we know the algo does what it's supposed to do we should see that our test has passed, and  yet  it fails. 

<img src="https://i.imgur.com/G19fZnG.png" width=300>

If we take a look at the **Test Summary** we can see as to why the test has failed. 


<img src="https://i.imgur.com/olGAYMm.png" width=300 />


So let's remedy that by importing the **flatten** function. 

```js
import flatten from './flatten'

it("should flatten an array of arrays", () => {
  const nestedArray = [1,[2,3],[4,5]];
  const flatArray = [1, 2, 3, 4, 5];
  expect(flatten(nestedArray)).toEqual(flatArray);
});
```

The test should pass now. 

<img src="https://i.imgur.com/pBR0Dzv.png" width=300/>

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Now it's your turn to create the following tests:

- it should return an empty array when the input is an empty array
- it should return a flattened array if the input contains 2 levels deep of nested arrays

**Bonus**
- it should confirm that the input type is an array

Hint: review the following: [expect.any(constructor)](https://jestjs.io/docs/expect#expectanyconstructor)

<hr> -->

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min

Now it's your turn to write some tests and test your algorithm skills. This time we are taking a  [Test Driven Development](https://learntdd.in/react/) approach. This means we write failing tests first and then the code to make them pass. 

- it should take in an array of duplicate elements and return an array of unique elements. 
- it should return an empty array when the input is an empty array

**Bonus**
* it should confirm that the input type is an array

Hint: review the following: [expect.any(constructor)](https://jestjs.io/docs/expect#expectanyconstructor)
<!-- - [test if object, array or string](https://github.com/facebook/jest/issues/3457) - 4th thread from bottom of page -->

<hr>

<!-- <details><summary>Solution</summary>

```js
it('should returns empty array when the input is an empty array', () => {
  // input
  const nestedArray = [];
  // expected output
  const flatArray = [];
  // match our expectations
  expect(flatten(nestedArray)).toEqual(flatArray);
});

it('should flatten an array that is at least 4 levels deep', () => {
  // input
  const nestedArray = [1, [2, 3], [[4, [5]]]];
  // expected output
  const flatArray = [1, 2, 3, 4, 5];
  // match our expectations
  expect(flatten(nestedArray)).toEqual(flatArray);
});

it('should determine input in an array', () => {
  // input
  const nestedArray = [];
  // expected output
  expect(nestedArray).toEqual(expect.any(Array));
});
```
</details> -->


### Test Suites
Being that these tests are meant to test the validity of the same code we could have placed them in a **describe()** so they are viewed as a suite of tests. 


```js
describe("flatten tests", () => {
  it("should flatten an array of arrays", () => {
    // ...code
  });

  it("should returns empty array when the input is an empty array", () => {
    // ...code
  });

  it("should flatten an array that is at least 4 levels deep", () => {
    // ...code
  });
});
```


## Testing Using The React Testing Library

Testing in React uses the same approach for creating individual tests and organizing them into a suite of tests.  

We do however need to leverage the [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/).  For even more advanced testing where we can't manipulate the DOM, we would need the assist of **Enzyme**. 

### Setup
Let's first create a filed called **App.test.js** and import **react**, the component we want to run test against, and both **render** and **screen** from the **React Testing** library.

```js
import React from 'react'
import App from './App';
import { render, screen } from '@testing-library/react';
```

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's take a minute to look at the documentation for [render](https://github.com/testing-library/react-testing-library) as it will hold the DOM elements and run the query as well as [screen](https://testing-library.com/docs/queries/about/#screen) which contains the DOM elements rendered by that component. 


<hr> -->

### Structure Of A Test

Testing React Components is a bit different than testing plain JS code as we did with our **flatten** algorithm.  The diagram below describes the basic steps needed to test a React Component. 

<img src="https://i.imgur.com/xLpJOex.png" width=500  />

### Writing A Basic Test

Our basic test will confirm that the text **"learn react"** is being rendered via the **App** component. 

 For that we will need to **render** the component and then query the page for the element that contains our text using **screen.getByText()**.


```js
import React from 'react'
import App from './App';
import { render, screen } from '@testing-library/react';

test('renders learn react link', () => {
  // RENDERS THE COMPONENT WE WANT TO TEST
  render(<App />);
  // FINDS THE ELEMENT WE WANT TO INTERACT WITH 
  const linkElement = screen.getByText(/learn react/i);
});
```

Our test appears to be failing. Why? 

<img src="https://i.imgur.com/buPaqk0.png" width=500  />

**Import The Library** 

So it looks like it's missing the **@testing-library/react** package so let's resolve that error by importing the library. 

<img src="https://i.imgur.com/fDmp7eg.png" width=300/>

And so our test now passes.

<img src="https://i.imgur.com/Q2cOm6H.png" width=500  />


Let's add a console log to see what **linkElement** returns.

```js
import React from 'react'
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
    // LETS SEE WHAT THIS RETURNS
  console.log('linkElement', linkElement)
});
```

**linkElement** 

<img src="https://i.imgur.com/y5JzQbb.png" width=500/>

In order to confirm that the test meets our expectations we still need to use the **expect()** function as before.  This time we will use an extended method called **[expect().toBeInTheDocument](https://github.com/testing-library/jest-dom#tobeinthedocument)**.

```js
import React from 'react'
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
    // LETS SEE WHAT THIS RETURNS
  console.log('linkElement', linkElement)
  // THE EXPECT METHOD TO CONFIRMS THAT THE TEXT IS IN THE DOCUMENT
  expect(linkElement).toBeInTheDocument();
});
```

It seems our test is failing. Why? 

<img src="https://i.imgur.com/IuoSsX0.png" width=500/>

Let's install the **testing-library/jest-dom** library and then import **import '@testing-library/jest-dom/extend-expect'** into the test file.

```
import React from 'react';
import App from './App';
import { render, screen } from '@testing-library/react';
import '@testing-library/jest-dom/extend-expect';
```

Now our test should pass.

<img src="https://i.imgur.com/3vVg5CJ.png" width=500/>


## Working with Enzyme
[Enzyme](https://github.com/airbnb/enzyme) mimics JQuery's DOM manipulation library to make testing React easier. Using Enzyme we can also directly test **state** within a class based component which the **React Testing Library** cannot do. It does not yet support testing **state** in functional components. 


### Setting Up Our Environment For Enzyme 
**Enzyme** requires that we first import the following packages:

- enzyme 
- enzyme-adapter-react-17-updated
- react-test-renderer
- @testing-library/jest-dom (previously imported)

At the moment, Enzyme has adapters that provide compatibility for different versions of React.  Since we are using the latest (v17) let's import that version. 

**Create setupTest.js file**


Then we need to create a **setUpTests.js** file. Create-react-app reads this file to see if there is any additional setup for the tests. In that file let's import the **jest-dom** library and then configure Enzyme to use an **Adapter**

```js
import '@testing-library/jest-dom';
import { configure } from 'enzyme'
import Adapter from 'enzyme-adapter-react-17-updated'

configure({ adapter: new Adapter() })

export default Adapter
```

We just need to keep in mind that we will need to import this file into any of our ***.test.js** files that require Enzyme. 

## Writing Tests Using Enzyme
Inside the **components** folder we will find both **Counter** and **HelloWorld**.  We will be using these folder to organize our code for testing. 

We will start with **HelloWorld** and need 2 files, one for our Component and the other to run our tests. 

- **src/components/HelloWorld/HelloWorld.js** 
- **src/components/HelloWorld/HelloWorld.test.js**

As before React will detect that there is a test but since there isn't anything in it nothing will happen. 

<img src="https://i.imgur.com/HW23nrb.png" width=400/>

### Testing Props

Were going to take a [Test Driven Development](https://learntdd.in/react/) approach now where we will write our tests first and then the code that will cause it to pass, or fail. 

Let's write a test that confirm the `HelloWorld` component renders out a name that is passed to it via props. 

Enzyme tests begin with rendering a React component, and for this, you have three choices: 

- Shallow Rendering
- Full DOM Rendering
- Static Rendering

Let's start with Shallow Rendering as it should be used for tests that are limited in scope to the component being tested and will not need to test lifecycle method nor render any of it's children. 

#### Initial Setup 

Let's start by importing **React**, the **Adapter**, [shallow](https://enzymejs.github.io/enzyme/docs/api/shallow.html) and the **HelloWorld** component. 
```js
import React from 'react'
import Adapter from '../../setUpTests'
import { shallow } from 'enzyme'
import HelloWorld from './HelloWorld'
```

Although we are creating a test to confirm a prop value we will also include additional tests so let's include a **describe** to group them into a test suite. 

```js
//...previous imports

describe('Hello world component', () => {
  it('should render props as expected', () => {

  })
})
```

Here we will be testing to confirm that the **HelloWorld** component was passed a prop value of **Your name**. 

```js
//...previous imports

describe('Hello world component', () => {
  it('should render props as expected', () => {
    // instantiate the component and pass in a prop
    const component = shallow(<HelloWorld name={'Your name'} />)
    expect(component.contains('Your name')).toBe(true)
  })
})
```

The testing engine should rerun automatically and this time the App and flatten tests passes but not HelloWorld. 

<img src="https://i.imgur.com/GM2dMu2.png" alt="" width=400 />

Of course the reason being that we haven't written the actual HelloWorld Component as of yet. 

Let's write the minimum amount of code needed for it to pass. In this example, we just need a component that renders **prop.name**.

```js
import React from 'react';

const HelloWorld = (props) => (
    <h1>{props.name}</h1>
)

export default HelloWorld;
```

The test passes without the need to import and run the component in App.

<img src="https://i.imgur.com/cN6ITBK.png" alt="" width=400 />

## Writing Tests for a Counter App 

For this exercise, you will be continue using **TDD** to write a failing test first and then the React code to make them pass. 

We want to build a counter app. When we press a button, we want a number stored in state to increase, and when we press a second button that number will decrease. Given these test requirements, write a React component that passes the following tests.

### Initial Setup
Let's add a **Counter.test.js** file 

- **src/components/Counter/Counter.test.js**

<!-- Copy the following code into the **Counter.js** component and we will write our tests to validate  this code. 

```js
import React, {useState} from 'react'

export default function Counter(props) {
  const [count, setCount] = useState(0)

  return (
      <div>
        <h1>Counter</h1>
        <div>Current Count: 
            <span className='counter'>{count}</span>
        </div>
        <section>
          <button className='plus' onClick={() => setCount(count + 1)}>+</button>
          <button className='minus'onClick={() => setCount(count - 1)}>-</button>
        </section>
      </div>
  )
}
``` -->


Copy the following code into **Counter.test.js** to get us started. 


```js
import React from 'react'
import Adapter from '../../setUpTests'
import { shallow } from 'enzyme'

import Counter from './Counter'

describe('Counter component', () => {

})
```

<!-- <hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 20min -->


Here are the functions that we will be using in case we want to review the [Jest](https://facebook.github.io/jest/docs/en/api.html) and [Enzyme](https://github.com/airbnb/enzyme/tree/master/docs/api) documentation and get a better idea of what they are doing. 

#### Jest

- [.toBe()](https://jestjs.io/docs/en/expect#tobevalue)
- [.toEqual()](https://jestjs.io/docs/en/expect#toequalvalue)

#### Enzyme
- [.contains()](https://github.com/enzymejs/enzyme/blob/master/docs/api/ShallowWrapper/contains.md) 
- [.find()](https://github.com/enzymejs/enzyme/blob/master/docs/api/ShallowWrapper/find.md)
- [.text()](https://github.com/enzymejs/enzyme/blob/master/docs/api/ShallowWrapper/text.md)
- [.simulate()](https://github.com/enzymejs/enzyme/blob/master/docs/api/ShallowWrapper/simulate.md)

### The Tests

Here are the tests we will create to test the Counter component and it's functionality. 

- should have a header that says "Counter"
- should display the current number in an element with the class name of **number**
- should have a button with a class name of **plus** that increases the number in state
- should have a button with a class name of  **minus** that decreases the number in state





#### The Header Test

If we examine the Counter component we can see that it contains an h1 with the text Counter and that is what we will run our test against. 


```js
describe('Counter component', () => {
  it('should have a header that says "Counter"', () => {
    const component = shallow(<Counter />)
    expect(component.contains(<h1>Counter</h1>)).toBe(true)
  })
})
```

The will fails as expected. 

<img src="https://i.imgur.com/6yGWDIk.png" alt="" width=400 />


 So now let's write the code needed to make it pass.  In the **Counter.js** file add the following:

```
import React from 'react';

export default function Counter(props) {

  return (
    <div>
      <h1>Counter</h1>
    </div>
  );
}
```

The test should now pass. 

<img src="https://i.imgur.com/ioufcXn.png" alt="" width=400 />

#### The Counter Test

Let's now have our Counter component render a span with a class of **counter** that should show the starting value. 

```js
describe('Counter component', () => {
  // ...previous tests

  it('should display the current number in an element with the className number', () => {
    const component = shallow(<Counter />)
    expect(component.find('.counter').text()).toEqual("0")
  })
})
```

Test should once again fails as expected so let's add the code to make it pass. This

```js
export default function Counter(props) {
  return (
    <div>
      <h1>Counter</h1>

      <div>
        Current Count:
        <span className="counter">0</span>
      </div>
    </div>
  );
}
```

Now it should passes. 


<img src="https://i.imgur.com/UVyPqxX.png" alt="" width=400 />



#### Adding beforeEach()

Since we will need to recreate the Counter component for each test we can create a shallow version of it prior to running each subsequent test. 

To do this we must use the **[beforeEach()](https://jestjs.io/docs/api#beforeeachfn-timeout)** function and then we update each test and remove the local shallow copy.

```js
import React from 'react'
import { shallow } from 'enzyme'

import Counter from './Counter'

describe('Counter component', () => {
  let component;
  beforeEach(() => {
    component = shallow(<Counter />)
  })

  it('should have a header that says "Counter"', () => {
    expect(component.contains(<h1>Counter</h1>)).toBe(true)
  })

  it('should display the current number in an element with the className of "number"', () => {
    expect(component.find('.counter').text()).toEqual("0")
  })

})
```

Now let's continue with our tests. 

#### The Increment Using Button Test

Testing buttons requires that we fire a **click**  event and cause it's functionality to execute.  We can do this using **.simulate()** and confirm that the value has increased by 1. 


```js
describe('Counter component', () => {
  let component
  beforeEach(() => {
    component = shallow(<Counter />)
  })

   // ...previous tests

  it('should have a button with a class plus that increases the number in state', () => {
    component.find('.plus').simulate('click')
    expect(component.find('.counter').text()).toEqual("1")
  })
})
```

This also requires that we update our Component to include a button but also **state**. 

```js
import React, { useState } from 'react';

export default function Counter(props) {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Counter</h1>

      <div>
        Current Count:
        <span className="counter">{count}</span>
      </div>

      <section>
        <button className="plus" onClick={() => setCount(count + 1)}>
          +
        </button>
      </section>
    </div>
  );
}

```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

#### The Decrement Using Button Test

Write the following test: 

- it should have a button with a class name of  **minus** that decreases the number in state



<hr>

<details><summary>Solution</summary>

```js
describe('Counter component', () => {
  let component
  beforeEach(() => {
    component = shallow(<Counter />)
  })

   // ...previous tests
  it('should have a button with a class minus that decreases the number in state', () => {
    component.find('.minus').simulate('click')
    expect(component.find('.counter').text()).toEqual("-1")
  })
})
```

</details>

[CodeSandbox Solution](https://codesandbox.io/s/rctr-react-testing-solution-2tvwm)


<!-- ## Bonus (Time Permitting): To Do List App 
As a bonus let's now create a **ToDo** list app using test driven development. First let's create our files.

We will have two components: a **ToDos.js** component which will hold individual **Todo.js** components.


- src/components/ToDos/ToDos.js
- src/components/ToDo/ToDo.js

And all of our tests will be performed on the ToDos component so lets create the test file.

- src/components/ToDos/ToDos.test.js

Now let's scaffold the configuration for our testing file.

**ToDos.test.js**

Let's add the following code to the test file. 

```js
import React from 'react'
import { mount } from 'enzyme'

import ToDos from './ToDos'
import ToDo from './ToDo'

describe('ToDos Component', () => {
  const listItems = [
    { task: 'create lesson', done: false },
    { task: 'clean apartment', done: false }
  ]

  let component
  beforeEach(() => {
    component = mount(<ToDos tasks={listItems} />)
  })

  // add tests here

})
```
This looks pretty similar to our other testing blocks, but this time in **beforeEach()** we will use **mount** instead of **shallow** since we are going to have subcomponents within our parent component.  

#### Counting Subcomponennts 

This time we will write our tests first and then the actual code that would validate the test. 

```js
it('should contain two todo subcomponents', () => {
  expect(component.find(ToDo).length).toBe(2)
})
```

Let's write the minimum amount of code to make this test pass:

**ToDos.js**
```js
import React  from 'react'

import ToDo from './ToDo'

function ToDos(props) {
    return (
      <div>
        {props.tasks.map( (task, idx) => 
          <ToDo task={task} key={idx} />
        )}
      </div>
    )
}

export default ToDos
```

**ToDo.js**
```js
import React from 'react'

const ToDo = ({ task }) => {
  return (
    <div>
      <div></div>
    </div>
  )
}

export default ToDo
```

#### Test Rendering The Todo Components

```js
  it('should render the todo list tasks', () => {
    component.find(ToDo).forEach((todo, idx) => {
      expect(todo.find('.task-name').text()).toBe(listItems[idx].task)
    })
  })
```

The code to pass this one is pretty minimal. 

**ToDo.js**
```js
import React from 'react'

const ToDo = ({ task }) => {
  return (
    <div>
      <div className='task-name'>{task.task}</div>
    </div>
  )
}

export default ToDo
```

Now let's create functionality for making a new list item.
```js
  it(`should have have a state attribute for the new todo that should update 
      when the user types in an input`, () => {
    expect(component.find('.input').text()).toEqual("")
    component.find('input').simulate('change', {target: {value: 'hello'}})
    expect(component.find('.input').text()).toEqual("hello")
  })
```
Note that we can mock events by adding targets and values to the **simulate** method! We normally access **e.target.value**, so we create a similar structure when we mock the event!

**ToDos.js**
```diff
function ToDos(props) {
  const [newTodo, setNewTodo] = useState('')

+  const handleChange = e => {
     setNewTodo(e.target.value)
+  }

    return (
      <div>
+        <input onChange={handleChange}/>
...
```
<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 20min

#### You Do: Finish To Do App 

Write the following tests. After writing a test, implement the React code to pass that test.
* **Should create a new todo on the click of a button and update the UI with it**

* **Should mark todos as done on the click of a button**



<details open>
<summary>Solution</summary>
<br>
  
ToDo.js
```js
import React from 'react'

const ToDo = ({ task, markComplete }) => {
  return (
    <div>
      <button className='mark-done' onClick={e => markComplete(task)}>Mark as Complete</button>
      <div className={`task-name ${task.done ? 'checked' : 'unchecked'}`}>{task.task}</div>
    </div>
  )
}

export default ToDo

```

ToDos.js
```js
import React, { useState } from 'react'

import ToDo from './ToDo'

function ToDos(props){
  const [newTodo, setNewTodo] = useState('')
  const [toDos, setToDos] = useState(props.tasks)

  const handleChange = e => {
    setNewTodo(e.target.value)
  }

  const createToDo = e => {
    setToDos([...toDos, {task: newTodo, done: false}])
    setNewTodo(e.target.value)
  }

  const markComplete = todo => {
    let toDosArray = [...toDos]
    let index = toDosArray.indexOf(todo)
    toDosArray[index].done = !toDosArray[index].done 
    setToDos(toDosArray)
  }

    return (
      <div>
        <input onChange={handleChange}/>
        <button onClick={createToDo} className='new-todo'>create</button>
        {toDos.map((task, idx) => 
          <ToDo task={task} markComplete={markComplete} key={idx} />
        )}
      </div>
    )
}

export default ToDos
```

ToDos.test.js
```js
import React from 'react'
import { mount } from 'enzyme'

import ToDos from './ToDos'
import ToDo from './ToDo'

describe('ToDos Component', () => {
  const listItems = [
    { task: 'create lesson', done: false },
    { task: 'clean apartment', done: false }
  ]

  let component
  beforeEach(() => {
    component = mount(<ToDos tasks={listItems} />)
  })

  it('Should contain two todo subcomponents', () => {
    expect(component.find(ToDo).length).toBe(2)
  })

  it('Should render the todo list tasks', () => {
    component.find(ToDo).forEach((todo, idx) => {
      expect(todo.find('.task-name').text()).toBe(listItems[idx].task)
    })
  })

  it(`Should have have a state attribute for the new todo that should update 
      when the user types in an input`, () => {
    component.find('input').simulate('change', {target: {value: 'hello'}})
     expect(component.find('input').contains('hello')).toBe(true)
  })

  it(`Should create a new todo on the click of a button and update the
    UI with it`, () => {
    component.find('.new-todo').simulate('click')
    expect(component.find(ToDo).length).toBe(3)
  })

  it('Should mark todos as done on the click of a button', () => {
    component.find('.mark-done').at(0).simulate('click')
    expect(component.find(ToDo).filter(task => task.done).length).toBe(1)
  })
})
```

</details> -->

<!-- 
## Review

* What is Jest? How about Enzyme?
* What is the difference between **shallow** and **mount**? -->

## Resources
- [React Testing Libraries](https://medium.com/javascript-in-plain-english/testing-in-react-part-2-react-testing-library-f32432b93c6c)
- [Beginner Guide To Testing React Apps](https://thomlom.dev/beginner-guide-testing-react-apps/)
- [Testing Functional Components Using Hooks](https://medium.com/@acesmndr/testing-react-functional-components-with-hooks-using-enzyme-f732124d320a)
- ['it' vs 'test'](https://stackoverflow.com/questions/45778192/what-is-the-difference-between-it-and-test-in-jest)
- [Jest](http://facebook.github.io/jest/)
- [Enzyme](https://github.com/airbnb/enzyme/tree/master/docs/api)
