# Learning React Hooks

Following React.js Hooks Crash Course: https://www.youtube.com/watch?v=-MlNBTSg_Ww


## General

### What are React Hooks?

With React Hooks we can manage state and achieve the same functionality as with lifecycle methods in functional components. We do not need to use classes anymore.

### Why should we use it?

Sharing (stateful) logic between components becomes easier


## Application

### How to manage state

useState(...) is a function we can import from React. It is also a so called hook.

useState(...) will always return an array with exactly 2 elements. The first one is a snapshot of the current state and the second one a function that will allow us to modify the state. We can name them as we want:

```
const [state, setState] = useState({
    ...state,
    selected: true,
    amount: 14,
    name: 'Bill'
});
```

**There is a major difference between the function useState gives us and the setState property we have from the state in classes.**
- setState in classes will modify or add whatever key-value pairs we pass and merge it with the current state. This is due because in a class we have only 1 state.
- When using hooks, the whole state is overwritten. Therefor we need to add ...state to not lose all current values. The state also doesn't need to be an object. It can by any data type. 

Alternatively, we can create multiple states:

```
const [selected, setSelected] = useState(true);

const [amount, setAmount] = useState(15);

const [name, setName] = useState('Bill');
```


### Lifecycle methods

useEffect(...) is a function we can import from React. It is also a so called hook. It is here to manage side effects such as HTTP requests.

useEffect(...) should be added in the functional component body after the state and takes two arguments, a function and an array of dependencies. It will be executed by React **after each render of the component.**

Also here we can use multiple useEffect(...)'s but to avoid redundancy only 1 should be used.

```
useEffect(() => {});        // without second argument, it will execute useEffect after each render

useEffect(() => {}, []);    // with an empty array as second argument, it will run only once and is the equivalent of componentDidMount

useEffect(() => {}, [props.selected, props.amount]);    // useEffect will run after the first render and then every time the dependencies are modified. In this case selected and amount

useEffect(() => {
    return () => {
        console.log('component did unmount');
    }
}, []);                     // useEffect(...) can return nothing or another function. If another function is declared, it will run before the next useEffect and should be used for cleaning up. Equivalent of componentWillUnmount 
```

