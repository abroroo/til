# How to prevent re-rendering in React? 

When you want to avoid re-redering some component, you can wrap it in __`React.memo()`__ method. It memoizes the component and prevents re-rendering when its props haven't changed.

```javascript
const MyComponent = React.memo(({ prop1, prop2 }) => {
    // Component logic
});


```
