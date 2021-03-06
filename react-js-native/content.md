class: center, middle

# react(-native|-js)

---

# Agenda

1. react principles
2. react-native
3. awesome
4. caveats
5. realistically

---

# React principles

![allthethings.jpeg](./img/allthethings.jpeg)

---

## Everything is a component!

![composition](./img/thinking-in-react-components.png)

--

(~= Angular's directives)

---

## Everything is a component!

![tree](./img/component-dom-tree.png)

---

# The rendering cycle in react

Anatomy of a React component:

* `render`, a function that kind of work as a template
* `props`, data passed from parent component
* `state`, the component internal, non leaky, data

--

`subtree DOM = render(props + state)`

---

# The rendering cycle in react

**There is no DOM mutation**, the **whole** app is re-rendered every time some component `state` changes.

--

> mrgmrglb performances?! you craaaazy?!

--

> JS is fast, DOM is slow.

--

React does it well:

1. generate a `virtual-DOM`,
1. diff it with previous `virtual-DOM`,
1. generate a list of minimal actual DOM changes,
1. Apply the changes

---

But a component is not just JS.

--

Right?

--

It also comes with markup (HTML) and style (CSS).

--

Right?

--

So we just put everything in the same file. JS, ~HTML~ and ~CSS~.

--

![dont-care.gif](./img/dont-care.gif)

--

Separation of concerns != separation of languages.

---

```jsx
import React, {div, span, button} from 'react';

class Counter extends React.Component {
  constructor() {
    super();
    this.state = {
      counter: 0
    };
  }

  render(){
    return (
      <div style={[ styles.background, styles.bottomBarMargin ]} >
        <span>{this.state.counter}</span>
        <button onClick={this.increment}>Click!</button>
      </div>
    );
  }

  increment = () => {
    this.setState({
      counter: counter + this.props.incrementBy
    });
  }
}

const styles = {
  bottomBarMargin:{
    marginBottom: 110,
  },
  background: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'space-around',
    backgroundColor: 'blue',
  },
};

export default Counter;

```
---

![eyes](./img/eyes.gif)

--


OK, all right, that's not your usual javascript file.

--

It's ES6 + JSX

You'll get used to it super quickly and will never want to come back.

---

# Inter component communication

* Parent > child : props
* Child > parent: functions passed as props

---

# Smart / dumb component principle

Smart components

* contain the logic to fetch data and apply actions
* usually have a `state`
* can nest both other smart components or dumb

Dumb components

* pure rendering logic based on props
* only nest other dumb components

---

# React Native

Exact same principles as React web

* components work exactly the same
* Javascript running live (not compiled to Objective-C)

--

but:

* the js file either come from the compiled bundle or... any URL
* the target is now native components instead of the DOM
* replace `div` with `View` and span with `Text`

That's it.

---

```jsx
import React, {View, Text, TouchableHighlight} from 'react-native';

class Counter extends React.Component {
  constructor() {
    super();
    this.state = {
      counter: 0
    };
  }

  render(){
    return (
      <View style={[ styles.background, styles.bottomBarMargin ]} >
        <Text>{this.state.counter}</Text>
        <TouchableHighlight onPress={this.increment}>
          <Text>Press me!</Text>
        </TouchableHighlight>
      </View>
    );
  }

  increment = () => {
    this.setState({
      counter: counter + this.props.incrementBy
    });
  }
}

const styles = {
  bottomBarMargin:{
    marginBottom: 110,
  },
  background: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'space-around',
    backgroundColor: 'blue',
  },
};

export default Counter;

```

---

Demo?
Live code?

---

# What's awesome with react(-native)

* The `react` principles are really great

--

* Learn `react` once, apply in web, iOS and soon Android envs

--

* Great developer experience: live reload, ES6, JSX, leverage JS ecosystem

--

* and, the most important

---

# Continuous deployment. On iOS. Yes Sire

> But, how do you bypass Apple review process?

Apple conditions don't allow apps to download and run code at runtime.

--

Unless

--

It's code that run in the javascript / web environment.

--

Because it can't really do anything harmful.

---

# Meh

You have to trust Facebook and the community to maintain `react-native` long enough.

That is all I can see.

---

# Ok, but, realistically?

We don't have to _switch_ to react native,
--
we can use it in specific some places.

--

* Use `react-native` to learn, A/B test
* Rewrite in Objective-C once it is stabilized
