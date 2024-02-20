# Case
When you have a div that is initially empty but gets polulated under some condition or on some button click
easy way to do testing in such cases is to store your test data in the object then use that object to test the actual code. 

### For example: you have a div that is populated on button click 

```javascript
import React, { useState } from "react";

const DynamicChildrenComponent = () => {
  const [children, setChildren] = useState([]);

  const handleButtonClick = () => {
    // Generate or update children array
    const newChildren = ["apple", "orange", "chair", "cell phone"];
    setChildren(newChildren);
  };

  return (
    <div>
      <button onClick={handleButtonClick}>Generate Children</button>
      <div data-test="label-container">
        {children.map((child, index) => (
          <div key={index}>{child}</div>
        ))}
      </div>
    </div>
  );
};

export default DynamicChildrenComponent;

```

# How to test it with cypress: seperate test case in an object or array of objects 

```javascript
const childrenData = [
  { index: 0, text: 'apple' },
  { index: 1, text: 'orange' },
  { index: 2, text: 'chair' },
  { index: 3, text: 'cell phone' }
];
```

### Then you can use that object and iterate over the div to test it with your stored test object 

```javascript
childrenData.forEach(({ index, text }) => {
  cy.get('[data-test="label-container"] > :nth-child(' + (index + 1) + ')')
    .should('contain.text', text);
});

```
