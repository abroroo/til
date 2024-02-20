# Case: Dynamic Population of Div on Button Click
When you've got a div that starts off empty but fills up based on certain conditions or user interactions, the best testing approach is to organize your test data and use it to validate the behavior of your code.

## Example Scenario:

Consider a scenario where you have a div that is populated with items when a button is clicked.

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

# How to Test it with Cypress:

To test this behavior with Cypress, you can organize your test data into an array of objects representing the expected children. Then, iterate over this array to validate each child in the div.

```javascript
const childrenData = [
  { index: 0, text: 'apple' },
  { index: 1, text: 'orange' },
  { index: 2, text: 'chair' },
  { index: 3, text: 'cell phone' }
];

// Iterate over the test data and validate each child
childrenData.forEach(({ index, text }) => {
  cy.get('[data-test="label-container"] > :nth-child(' + (index + 1) + ')')
    .should('contain.text', text);
});

```

This approach ensures that your test cases remain organized and scalable, allowing you to easily validate the dynamic behavior of your component.
