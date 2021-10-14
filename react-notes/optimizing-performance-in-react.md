# Optimizing Performance in React

## Performance Tools in React

### React-addons-perf

```jsx
import Perf from 'react-addons-perf'; 
Perf.start() 
// App 
Perf.stop()
```

The Perf methods can be used to take performance measurements.

* `Perf.printInclusive()` prints overall time taken.
* `Perf.printExclusive()` prints time excluding mounting time
* `Perf.printWasted()` prints time wasted on components that didn't actually render anything.
* `Perf.printOperations()` prints all DOM manipulations
* `Perf.getLastMeasurements()` prints the measurement from the last Perf session.

### Avoid Reconciliation

#### shouldComponentUpdate()

```jsx
shouldComponentUpdate(nextProps, nextState) {
 return this.props.color !== nextProps.color;
}
```

Here we use a shallow comparison to determine if the props of the component have changed. If so, the component should update.

#### React.PureComponent

This is a React component that implements `shouldComponentUpdate()` and only diffs and updates when it returns `true`. Any child of `PureComponent `must also be a `PureComponent`.

```jsx
class CounterButton extends React.PureComponent {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }
  render() {
    return (
      <button
       color={this.props.color}
       onClick={() => this.setState(state => ({count: state.count + 1}))}>
       Count: {this.state.count}
      </button>
    );
  }
}
```

### Other hooks

#### useReducer

This is an alternative to useState. Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a `dispatch` method.

Cases to use useReducer over useState:

1. Complex state logic that involves multiple sub-values
2. The next state depends on the previous one
3. Optimize performance for components that trigger deep updates by [passing `dispatch` down instead of callbacks.](https://reactjs.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down)

```jsx
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

{% hint style="info" %}
The `dispatch` function identity is stable and won't change on re-renders.
{% endhint %}

#### useCallback

This returns a memoized callback that only changes if one of the dependencies has changed. This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. `shouldComponentUpdate`).

```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

{% hint style="info" %}
`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps).`
{% endhint %}

## Not Mutating Data

### Code examples

Consider this example:

```jsx
class ListOfWords extends React.PureComponent {
  render() {
    return <div>{this.props.words.join(',')}</div>;
  }
}

class WordAdder extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      words: ['hello']
    };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    // This section is bad style and causes a bug
    const words = this.state.words;
    words.push('world');
    this.setState({words: words});
  }

  render() {
    return (
      <div>
        <button onClick={this.handleClick} />
        <ListOfWords words={this.state.words} />
      </div>
    );
  }
}
```

{% hint style="info" %}
This example creates a bug and "world" is not actually displayed
{% endhint %}

To solve this problem, we should avoid mutating values that we are using as props or state.

One solution using `concat` can be:

```jsx
handleClick() {
  this.setState(state => ({
    words: state.words.concat(['world'])
  }));
}
```

Or we can use the spread operator in ES6:

```jsx
handleClick() {
  this.setState(state => ({
    words: [...state.words, 'world'],
  }));
};
```

For objects, we can also write code to avoid mutating objects. This is the way in which we mutate an object:

```jsx
function updateColorMap(colormap) {
  colormap.right = 'blue';
}
```

However, we can avoid mutating the original object using `Object.assign` in ES6:

```jsx
function updateColorMap(colormap) {
  return Object.assign({}, colormap, {right: 'blue'});
}
```

Or, we can use the spread operator for objects from ES2018:

```jsx
function updateColorMap(colormap) {
  return {...colormap, right: 'blue'};
}
```

### Immer

{% embed url="https://immerjs.github.io/immer" %}

{% embed url="https://github.com/immerjs/immer" %}

This is the basic syntax using Immer to avoid mutating data:

```jsx
import produce from "immer"

const nextState = produce(baseState, draft => {
    draft[1].done = true
    draft.push({title: "Tweet about it"})
})
```

#### useState + Immer

Here is an example on [CodeSandbox](https://codesandbox.io/s/immer-usestate-ujkgg?file=/src/index.js) that uses the hook useState and Immer together.

```jsx
import React, { useCallback, useState } from "react";
import produce from "immer";

const TodoList = () => {
  const [todos, setTodos] = useState([
    {
      id: "React",
      title: "Learn React",
      done: true
    },
    {
      id: "Immer",
      title: "Try Immer",
      done: false
    }
  ]);

  const handleToggle = useCallback((id) => {
    setTodos(
      produce((draft) => {
        const todo = draft.find((todo) => todo.id === id);
        todo.done = !todo.done;
      })
    );
  }, []);

  const handleAdd = useCallback(() => {
    setTodos(
      produce((draft) => {
        draft.push({
          id: "todo_" + Math.random(),
          title: "A new todo",
          done: false
        });
      })
    );
  }, []);

  return (<div>{*/ See CodeSandbox */}</div>)
}
```

{% embed url="https://codesandbox.io/s/immer-usestate-ujkgg?file=%2Fsrc%2Findex.js" %}

#### useImmer

The state updaters have the same pattern, so they can be simplified to using the [user-immer](https://www.npmjs.com/package/use-immer) package.

```jsx
import React, { useCallback } from "react";
import { useImmer } from "use-immer";

const TodoList = () => {
  const [todos, setTodos] = useImmer([
    {
      id: "React",
      title: "Learn React",
      done: true
    },
    {
      id: "Immer",
      title: "Try Immer",
      done: false
    }
  ]);

  const handleToggle = useCallback((id) => {
    setTodos((draft) => {
      const todo = draft.find((todo) => todo.id === id);
      todo.done = !todo.done;
    });
  }, []);

  const handleAdd = useCallback(() => {
    setTodos((draft) => {
      draft.push({
        id: "todo_" + Math.random(),
        title: "A new todo",
        done: false
      });
    });
  }, []);

  // SeeCodeSandbox 
```

{% embed url="https://codesandbox.io/s/use-immer-bvd5v?file=%2Fsrc%2Findex.js" %}

#### useReducer and Redux + Immer

Similar to `useState`, Immer also combines with `useReducer`. And we have `useImmerReducer` method from the use-immer package.

For Redux + Immer, refer to this doc of Redux Toolkit:

{% embed url="https://redux-toolkit.js.org/usage/immer-reducers" %}

### Other readings on immutable data

{% embed url="https://redux.js.org/faq/immutable-data" %}

{% embed url="https://www.codementor.io/blog/react-optimization-5wiwjnf9hj" %}

{% embed url="https://www.toptal.com/react/optimizing-react-performance" %}

