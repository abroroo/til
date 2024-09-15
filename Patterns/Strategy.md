# Strategy pattern (elegant replacement for if-else)

**What is the Strategy Pattern?**

When ther are multiple ways to do something, Strategy pattern allows to switch between them easily without changing the main code. Like different ways to validate input, fetch data, or animate elements. It helps keep your code organized and easy to manage.

**When to Use in Frontend?**

- **Form Validation:** Apply different validation rules on the fly.
- **Data Fetching:** Switch between APIs or data formats.
- **Animations:** Change animation styles based on settings.
- **Feature Toggles:** Turn features on or off at runtime.

---

**You can use the Strategy Pattern in functional programming.**

In functional programming, functions are first-class citizens—you can pass them around just like any other variable. This makes implementing the Strategy Pattern straightforward because you can use functions as interchangeable algorithms.

---

**Example in: Form Validation**

*Let's apply this to form validation.*

**1. Define Validation Strategies**

```javascript
const isEmail = (value) => /\S+@\S+\.\S+/.test(value);
const isPasswordStrong = (value) => value.length >= 6;
const isUsernameValid = (value) => /^[a-zA-Z0-9]+$/.test(value);
```

**2. Context Function**

```javascript
const validate = (value, validationStrategy) => validationStrategy(value);
```

**3. Using the Validation Strategies**

```javascript
console.log(validate('user@example.com', isEmail));       // true
console.log(validate('pass123', isPasswordStrong));       // true
console.log(validate('user_name', isUsernameValid));      // false
```

---

**Conclusion**

In functional programming, using the Strategy Pattern is natural and efficient. By passing functions as arguments, you can easily swap out algorithms or behaviors at runtime. This keeps your code clean, flexible, and easy to maintain.

---

**Class Example: Form Validation Strategies**

*Let's say we have input fields that need different validation methods.*

**1. Strategy Interface**

```typescript
interface ValidationStrategy {
  validate(value: string): boolean;
}
```

**2. Concrete Strategies**

```typescript
class EmailValidation implements ValidationStrategy {
  validate(value: string): boolean {
    return /\S+@\S+\.\S+/.test(value);
  }
}

class PasswordValidation implements ValidationStrategy {
  validate(value: string): boolean {
    return value.length >= 6;
  }
}

class UsernameValidation implements ValidationStrategy {
  validate(value: string): boolean {
    return /^[a-zA-Z0-9]+$/.test(value);
  }
}
```

**3. Context Class**

```typescript
class InputField {
  private strategy: ValidationStrategy;

  constructor(strategy: ValidationStrategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy: ValidationStrategy): void {
    this.strategy = strategy;
  }

  validate(value: string): boolean {
    return this.strategy.validate(value);
  }
}
```

**4. Using the Strategy**

```typescript
const emailField = new InputField(new EmailValidation());
console.log(emailField.validate('user@example.com')); // true

const passwordField = new InputField(new PasswordValidation());
console.log(passwordField.validate('pass123')); // true

// Change validation strategy at runtime
passwordField.setStrategy(new UsernameValidation());
console.log(passwordField.validate('user_name')); // false
```

---

