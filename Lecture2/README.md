# LESSON TWO LECTURE NOTES
## [@1m17s](https://youtu.be/FQPowZglpJA?t=1m17s) **ES6 Feature: "Arrow" Functions & Lexical `this`**
- Arrows are a shortcut syntax for writing functions
- Arrow functions have _some_ different behavior
- https://babeljs.io
- ES6 & ES2015 are the same thing
- The Arrow: `=>`
- The Arrow and lexical `this`:
  > Unlike functions, arrows share the same lexical `this` as their surrounding code. If an arrow is inside another function, it shares the “arguments” variable of its parent function.
  - https://babeljs.io/learn-es2015/#ecmascript-2015-features-arrows-and-lexical-this

  #### [@2m56s](https://youtu.be/FQPowZglpJA?t=2m56s) **Arrow Function Examples**
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // prints each array item
  numbers.forEach(num => {
    console.log(num);
  })
  ```
  - syntax: `argument arrow {curly braces}`

  #### [@4m1s](https://youtu.be/FQPowZglpJA?t=4m1s)
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // prints each array item and index position
  numbers.forEach((num, i) => {
    console.log(num, i);
  })
  ```
  - syntax `((multiple, arguments, passed, in) => { side_effect_or_return_value; })`
  - OT: Q: how does `=>` know `i` is the index?
    - A: it doesn't, it's a [forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach?v=example) thing: the second parameter is index.)

  #### [@4m38s](https://youtu.be/FQPowZglpJA?t=4m38s)
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // map duplicates value from numbers array
  const doubleNums = numbers.map(num => num * 2);
  // ---> [ 2, 4, 6, 8, 10 ]
  console.log(doubleNums)
  ```
  - Without curly braces a single statement is returned by default:
  - syntax: `(variable_name(s) => single_expression_return_value )`
  - note on map: doesn't modify the original array, just makes a copy

  #### [@7m50s](https://youtu.be/FQPowZglpJA?t=7m50s) **The equivalent functional version of the previous example**
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // map duplicates value from numbers array
  const doubleNums = numbers.map(function (num) {
    return num * 2;
  });
  // ---> [ 2, 4, 6, 8, 10 ]
  console.log(doubleNums)
  ```

## [@8m45s](https://youtu.be/FQPowZglpJA?t=8m45s) **Lexical `this`**
- example: https://jsbin.com/xivinos/10/edit?js,console
- **Functional Notation**
  - `this` is bound to the function
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // prints each array item
  numbers.forEach(function (num) {
    console.log(this);
  })
  ```

- **Arrow Notation**
  - an arrow function doesn't have it's own `this`
  - the arrow function's `this` references to it's parent, either global or the enclosing function's `this`
  ```js
  const numbers = [ 1, 2, 3, 4, 5 ];
  // prints each array item
  numbers.forEach(num => {
    console.log(this);
  })
  ```
  - e.g. the arrow function inside foo() refers to foo()'s `this`
  ```js
  function foo() { this }    // <--- references inside the function

  const bar = () => { this } // <--- references to the global
  ```

## [@10m25s](https://youtu.be/FQPowZglpJA?t=10m25s) **Bind**
- per [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind):
  > The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
- see also [this answer](https://stackoverflow.com/a/10115970/5225057)
```js
function sayHi() {
  console.log(this.name)
}

sayHi(); // <--- nothing gets printes
```

- the `bind()` method allows us to explicitly set what `this` refers to inside of a function
```js
function sayHi() {
  console.log(this.name)
}

const me = {
  name: 'Ben'
};

const boundSayHi = sayHi.bind(me);

boundSayHi(); // ---> Ben
```

  #### [@11m55s](https://youtu.be/FQPowZglpJA?t=10m25s) **Bind use cases**
  - NOTE: bind() doesn't need to invoke the method being bound, e.g.
    - me.sayHi.bind(...) not me.sayHi(bind(...))
  ```js
  const me = {
    name: 'Ben'
  };

  me.sayHi = function() {           // <--- what we've seen before
    console.log(this.name)
  }

  me.sayHi();   // ---> Ben

  const boundSayHi = me.sayHi.bind({  // <--- the bind() method
    name: 'Austen'
  });

  boundSayHi(); // ---> Austen
  ```

  #### [@14m](https://youtu.be/FQPowZglpJA?t=14m) **Q & A**

## [@15m](https://youtu.be/FQPowZglpJA?t=15m) **React Project: State**
- `create-react-app state`
- "State" is a key part of React
- React components are like custom HTML elements
- State is how you monitor what state the element is in
- Tracking current state conditions and basing behavior on those state consitions

## [@17m8s](https://youtu.be/FQPowZglpJA?t=17m8s) **Building a Counter**
- clear out the default App contents and unused logo import.
- start with a static component (no state), Header.js
- [App.js](Lecture2/state/src/App.js)
- [Header.js](Lecture2/state/src/Header.js)
- [App.css](Lecture2/state/src/App.css)

## [@20m45s](https://youtu.be/FQPowZglpJA?t=20m45s) **Simplifying the Code with function(props)**
- instead of a class:
  ```jsx
  import React, { Component } from 'react';
  import './App.css';

  export default class Header extends Component {
    render() {
      return (
        <div className='Header'>
          Our Header
        </div>
      );
    }
  }
  ```
- we can write Header.js as a function with `props`:
  ```jsx
  import React from 'react';
  import './App.css';

  export default function(props) { // <--- props for "properties"
    return (
      <div className='Header'>
        Our Header
      </div>
    );
  }
  ```

  #### [@22m34s](https://youtu.be/FQPowZglpJA?t=22m34s) **function(props) use case**
  - in App.js we can add:
  ```jsx
  import React, { Component } from 'react';
  // import logo from './logo.svg';
  import './App.css';
  import Header from './Header';

  class App extends Component {
    render() {
      return (
        <div className="App">
          <Header title={'My Functional Component'}/> //<--- title "property"
        </div>
      );
    }
  }

  export default App;
  ```

  - in Header.js we add the props!
  ```jsx
  import React from 'react';
  import './App.css';

  export default function(props) {
    return (
      <div className='Header'>
        {props.title} // <------------ add title property
      </div>
    );
  }
  ```

  - NOTE: `<h1>` has some margin built into it so that is why there is the buffer at the top (like in Homework1)

## [@23m54s](https://youtu.be/FQPowZglpJA?t=23m54s) **A Functional Component With State**
- A button, you push it, the counter goes up!
- [Counter.js](Lecture2/state/src/Counter.js) will be built as a class:
  ```js
  import React, { Component } from 'react';

  export default class Counter extends Component {
    render () {
      return (
        <div>
          a counter
        </div>
      );
    }
  }
  ```

#### [@24m20s](https://youtu.be/FQPowZglpJA?t=24m20s) **Q & A**

## [@26m40s](https://youtu.be/FQPowZglpJA?t=26m40s) **A Functional Component With State, cont.**
- [Counter.js](Lecture2/state/src/Counter.js)
- Import the Counter in src/App.js and stick the component in the App return

## [@28m12s](https://youtu.be/FQPowZglpJA?t=28m12s) **CONSTRUCTOR**
- we have a STATE object that is conected to the COMPONENT
- on that STATE object we can attach a count PROPERTY
- We can reference the PROPERTY inside of the RENDER method
- Initialize the default value with the constructor() method
- Constructor is a method that is in all ES6 classes
  ```js
  constructor(props) {
    super(props);
    this.state = {};
  }
  ```

## [@31m12s](https://youtu.be/FQPowZglpJA?t=31m12s) **Add the Button Functionality**
- custom method to add button clicking functionality
- onCick
- binding the method to the class
  ```js
  this.incrementCount = this.incrementCount.bind(this);
  ```

  - Could do it like this, but then we'd need to bind each instance of the function being invoked:
  ```js
  <button onClick={this.incrementCount.bind(this)} >Increment</button>
  ```

## [@38m17s](https://youtu.be/FQPowZglpJA?t=31m12s) **Update the State**
- modify the state in a way which tells react to update the component
```js
incrementCount() {
  // alert(this.state.count);
  this.state.count++;       // <--- view in browser JS console
  console.log(this.state)   // <--- count increases, but not rendered!
}
```

- Instead we use: `this.setState({ count: this.state.count + 1 })`
- and the button clicks update the State and the new State is rendered in the html!

## [@42m42s](https://youtu.be/FQPowZglpJA?t=42m42s) **Update the State with a callback**
- setState is ASYNCHRONOUS
- setState can take an object or a callback function as its argument.
- better practice is to use arrow functions for a callback when you need to reference the current state to generate or get to the updated state, e.g.
```js
this.setState(currentState => {
  return {
    count: currentState.count + 1
  }
});
```

***
## fin
