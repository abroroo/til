# Chain of Responsibility Pattern

### **What's the Chain of Responsibility Pattern?**

The Chain of Responsibility Pattern is like passing a request along a line of handlers until someone takes care of it. It allows you to send data through a chain of functions, where each function decides whether to handle the data or pass it to the next one.

**Think of it this way:** You have a complaint, and you talk to customer service. If they can't help, they pass you to a manager, and so on, until someone resolves your issue.

---

### **Why Use the Chain of Responsibility Pattern?**

- **Flexible Handling:** Multiple handlers can process the request one after another.
- **Decoupling:** The sender doesn't need to know who will handle the request.
- **Easy to Modify:** Add or remove handlers without changing much code.

### **When to Use the Chain of Responsibility Pattern**

- **Form Validation:** Validate input fields with multiple rules.
- **Middleware:** In libraries like Redux, actions pass through middleware functions.
- **Event Processing:** Handling events with multiple functions in order.

---

### **Example**

*Let's say we have a form that needs to go through multiple validation checks.*

**1. Create Validation Functions**

Each function checks a condition and decides to handle it or pass it on.

```javascript
const checkNotEmpty = (value, next) => {
  if (value.trim() === '') {
    return 'Input is empty';
  } else {
    return next(value);
  }
};

const checkIsEmail = (value, next) => {
  const emailPattern = /\S+@\S+\.\S+/;
  if (!emailPattern.test(value)) {
    return 'Invalid email format';
  } else {
    return next(value);
  }
};

const checkMaxLength = (maxLength) => (value, next) => {
  if (value.length > maxLength) {
    return `Input exceeds ${maxLength} characters`;
  } else {
    return next(value);
  }
};
```

**2. Chain the Validators**

Create a function to chain validators together.

```javascript
const chainValidators = (...validators) => {
  return validators.reduce((prev, current) => {
    return (value) => prev(value, (val) => current(val, (v) => v));
  });
};
```

**3. Use the Chain**

```javascript
const validateInput = chainValidators(
  checkNotEmpty,
  checkIsEmail,
  checkMaxLength(50)
);

console.log(validateInput('user@example.com')); // Output: 'user@example.com'

console.log(validateInput('')); // Output: 'Input is empty'

console.log(validateInput('invalid-email')); // Output: 'Invalid email format'
```



### **In Simple Words**

- **Chain of Responsibility is like a series of checkpoints:** Each function checks something and decides to handle it or pass it on.
- **You can create a pipeline of functions that process data step by step.**

---

