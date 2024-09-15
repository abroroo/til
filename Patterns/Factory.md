**Factory and Abstract Factory Patterns**

---

# **Factory Pattern**

**What's the Factory Pattern?**

The Factory Pattern is like having a special function that creates objects for you. Instead of using `new` to make objects, you call this function, and it gives you the object you need.

**Why use it?**

- **Simpler Object Creation:** You don't have to remember how to make the object.
- **Flexibility:** Decide which object to create while your program is running.
- **Organized Code:** Keep the creation code in one place.

**Functional Example in Frontend**

*Creating different shapes using factory functions:*

```javascript
// Functions to create shapes
const createCircle = (radius) => ({
  type: 'circle',
  radius,
  draw: () => console.log(`Drawing circle with radius ${radius}`),
});

const createSquare = (side) => ({
  type: 'square',
  side,
  draw: () => console.log(`Drawing square with side ${side}`),
});

// Factory function
const shapeFactory = (type, dimensions) => {
  if (type === 'circle') {
    return createCircle(dimensions.radius);
  } else if (type === 'square') {
    return createSquare(dimensions.side);
  } else {
    throw new Error('Unknown shape type');
  }
};

// Using the factory
const myCircle = shapeFactory('circle', { radius: 5 });
myCircle.draw(); // Output: Drawing circle with radius 5

const mySquare = shapeFactory('square', { side: 4 });
mySquare.draw(); // Output: Drawing square with side 4
```

---

# **Abstract Factory Pattern**

**What's the Abstract Factory Pattern?**

Think of it as a factory that creates other factories. It's useful when you need to create groups of related objects, like themed components in your app.

**Why use it?**

- **Create Related Objects Together:** Ensure that you use matching components.
- **Easily Switch Groups:** Change the whole group by changing the factory.
- **Clean Code:** Hide complex creation details.

**Functional Example in Frontend**

*Creating themed UI components:*

```javascript
// Component creators based on theme
const createButton = (theme) => (label) => ({
  type: 'button',
  theme,
  label,
  render: () => console.log(`Rendering ${theme} button: ${label}`),
});

const createInput = (theme) => (placeholder) => ({
  type: 'input',
  theme,
  placeholder,
  render: () => console.log(`Rendering ${theme} input: ${placeholder}`),
});

// Abstract factory function
const createUIFactory = (theme) => ({
  createButton: createButton(theme),
  createInput: createInput(theme),
});

// Using the abstract factory
const darkUIFactory = createUIFactory('dark');

const darkButton = darkUIFactory.createButton('Submit');
darkButton.render(); // Output: Rendering dark button: Submit

const darkInput = darkUIFactory.createInput('Username');
darkInput.render(); // Output: Rendering dark input: Username

// Switching to light theme
const lightUIFactory = createUIFactory('light');

const lightButton = lightUIFactory.createButton('Submit');
lightButton.render(); // Output: Rendering light button: Submit
```

---

### **In Simple Words**

- **Factory Pattern:** Use a function to create objects for you. You just tell it what you want, and it gives it to you.

- **Abstract Factory Pattern:** Use a function that gives you other functions to create a set of related objects, like all components for a dark theme.

---
