# How to prevent re-rendering in React?  (put them in cache)   

1. When you don't want a component to keep rerendering unnecessarily, you can use __`React.memo()`__. It basically remembers the component and stops it from rerendering unless its props change.  
 
```javascript
const MyComponent = React.memo(({ prop1, prop2 }) => {
    // Component logic
});


```
2. Use __`useMemo()`__ to calculate only when needed or once. It caches the result of a calculation and only recalculates when the inputs change.   
 
```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

```
3. Use __`useCallback()`__ to lock in event handlers or any callback functions. It ensures they don't get recreated on every render.  In React, when you define a function inside a component, like const `handleClick = () => { // Handle click logic }`, it gets recreated on each render. This means that every time your component rerenders, a new function with a new reference is created, even if the function's logic remains the same. `useCallback()` helps to prevent that. 

```javascript
const handleClick = useCallback(() => {
    // Handle click logic
}, []); // Empty dependency array

```


4. Optimize __`useEffect()`__: If you only want an effect to run once, just pass an empty dependency array [] as the second argument to __`useEffect()`__. It's like saying, "Only do this once, okay?"  

```javascript
useEffect(() => {
    // Effect logic
}, []); // Empty dependency array

```

5. No More Inline Functions: Don't declare functions inside the render method unless you want them recreated each time. Move them outside to keep them steady. 

```javascript
const handleClick = () => {
    // Handle click logic
};

const MyComponent = () => {
    return <button onClick={handleClick}>Click me</button>;
};

``` 

