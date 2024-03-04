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
