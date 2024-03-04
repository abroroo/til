# How to prevent re-rendering in React? 

1. When you want to avoid re-redering some component, you can wrap it in __`React.memo()`__ method. It memoizes the component and prevents re-rendering when its props haven't changed.

```javascript
const MyComponent = React.memo(({ prop1, prop2 }) => {
    // Component logic
});


```

2. Optimize __`useEffect()`__ Hooks: Provide an empty dependency array [] as the second argument to `useEffect()` to ensure that the effect runs only once, similar to `componentDidMount()` in class components.

```javascript
useEffect(() => {
    // Effect logic
}, []); // Empty dependency array


```

3. Avoid Inline Function Declarations: Define functions outside of the render method to prevent them from being recreated on each render.

```javascript
const handleClick = () => {
    // Handle click logic
};

const MyComponent = () => {
    return <button onClick={handleClick}>Click me</button>;
};

```
4. Use __`useCallback()`__: Memoize event handlers or any callback functions using __`useCallback()`__ to prevent them from being recreated on each render.

```javascript
const handleClick = useCallback(() => {
    // Handle click logic
}, []); // Empty dependency array

```
5. Use __`useMemo()`__ to calculate only when needed or once. `useMemo()` is a hook used to memoize the result of a computation. It takes a function and an array of dependencies, and it returns a memoized value. The function is only re-executed if one of the dependencies has changed. It's useful for optimizing expensive calculations.
