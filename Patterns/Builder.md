# Builder pattern *(let's build step by step, no need to build initially)*


**What is the Builder Pattern?**

Builder Pattern helps to create complex objects step by step using functions instead of defining the object intially. Each function adds or modifies a part of the object and returns a new object. 

---

**Key Points**

- **Immutable Objects:** Each function returns a new object, original stays unchanged.
- **No Classes Needed:** Simpler code without extra classes.
- **Composable Functions:** Easy to add or remove steps.

---

**Exaple: Cutomized Button**

*Let's create a button component that can have various optional features.*

**1. Start with a Base Object**

Create a default button object.

```javascript
const baseButton = {
  label: '',
  color: undefined,
  size: undefined,
  icon: undefined,
  onClick: undefined,
};
```

**2. Create Builder Functions**

Each function takes the current button and returns a new one with an added or changed property.

```javascript
const setLabel = (label) => (button) => ({
  ...button,
  label,
});

const setColor = (color) => (button) => ({
  ...button,
  color,
});

const setSize = (size) => (button) => ({
  ...button,
  size,
});

const setIcon = (icon) => (button) => ({
  ...button,
  icon,
});

const setOnClick = (onClick) => (button) => ({
  ...button,
  onClick,
});
```

**3. Build the Button Using Function Composition**

Chain the builder functions to construct your button.

```javascript
const buildButton = (...funcs) => funcs.reduce((acc, func) => func(acc), baseButton);
```

**4. Use the Builder Functions**

```javascript
const saveButton = buildButton(
  setLabel('Save'),
  setColor('green'),
  setSize('medium'),
  setIcon('save-icon'),
  setOnClick(() => console.log('Saved!'))
);

console.log(saveButton);
// Output:
// {
//   label: 'Save',
//   color: 'green',
//   size: 'medium',
//   icon: 'save-icon',
//   onClick: [Function],
// }
```

**5. Render the Button**

```javascript
const renderButton = (button) => {
  console.log(`Rendering button: ${button.label}`);
  if (button.color) console.log(`Color: ${button.color}`);
  if (button.size) console.log(`Size: ${button.size}`);
  if (button.icon) console.log(`Icon: ${button.icon}`);
  // Add event listener for onClick if needed
};

renderButton(saveButton);
// Output:
// Rendering button: Save
// Color: green
// Size: medium
// Icon: save-icon
```


---



