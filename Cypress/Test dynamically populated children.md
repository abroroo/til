## Case
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
      <div>
        {children.map((child, index) => (
          <div key={index}>{child}</div>
        ))}
      </div>
    </div>
  );
};

export default DynamicChildrenComponent;


```
