# Adapter Pattern

### **What's the Adapter Pattern?**

The Adapter Pattern is like a bridge between two pieces of code that don't normally work together. It allows you to use a class or function with an interface (methods and properties) that is different from what your code expects.

**Think of it this way:** You have a plug that doesn't fit into the socket. You use an adapter to connect them.

---

### **Why Use the Adapter Pattern?**

- **Compatibility:** Makes incompatible code work together.
- **Reusability:** Use existing code without modifying it.
- **Clean Code:** Keep your codebase organized by separating concerns.

---

### **Functional Example in Frontend Development**

*Let's say you have a new logging system, but your app is built to use the old one. We'll create an adapter to make them work together.*

**1. Existing Code Expects Old Logger**

Your app expects a logger with a specific interface:

```javascript
// Expected old logger interface
function logMessage(message) {
  console.log(`Log: ${message}`);
}
```

**2. New Logger Has a Different Interface**

The new logger uses a different method:

```javascript
// New logger with different interface
const newLogger = {
  write: (message) => console.log(`New Log: ${message}`),
};
```

**3. Create an Adapter Function**

We'll create an adapter that makes the new logger compatible with the old interface.

```javascript
function logAdapter(message) {
  newLogger.write(message);
}
```

**4. Use the Adapter in Your Code**

Now, you can use `logAdapter` wherever `logMessage` was used.

```javascript
// Original function that uses old logger
function processData(data) {
  // ... process data
  logMessage('Data processed.');
}

// Replace old logger with adapter
function processDataWithAdapter(data) {
  // ... process data
  logAdapter('Data processed.');
}

processDataWithAdapter({ name: 'John' });
// Output: New Log: Data processed.
```


### **Another Example: Fetch API Adapter**

*Suppose your code uses `axios` for HTTP requests, but you want to switch to the Fetch API without changing all your code.*

**1. Existing Code Uses Axios**

```javascript
// Function that uses axios
function getData(url) {
  return axios.get(url).then((response) => response.data);
}
```

**2. Create an Adapter for Fetch**

```javascript
function fetchAdapter(url) {
  return fetch(url).then((response) => response.json());
}
```

**3. Replace Axios with Adapter**

```javascript
// Replace axios.get with fetchAdapter
function getDataWithAdapter(url) {
  return fetchAdapter(url);
}

getDataWithAdapter('https://api.example.com/data').then((data) => {
  console.log(data);
});
```

---

### **When to Use the Adapter Pattern in Frontend**

- **Integrating Third-Party Libraries:** When a library doesn't match your expected interface.
- **Legacy Code:** Making old code work with new systems.
- **API Changes:** Adapting to changes in APIs without rewriting your code.

---

### **In Simple Words**

- **Adapter Pattern is a translator:** It converts code from one format to another so different parts can work together.
- **You write a small piece of code (adapter) that sits in between two systems.**

---

