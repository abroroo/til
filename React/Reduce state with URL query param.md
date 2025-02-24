When have a list with filters, and you want to keep active filters even if user refreshes the page or shares the link.

In React, we often do it using "state." But if the page reloads, this state resets, and we forget which filters were applied.

To fix this, we can use the URL (the web address) to remember the state.

Here's how we can do it:

1. **Sync State with URL:** When the user searches for something, we update the URL to include this searchString. This way, the URL always shows what's currently filtered or being searched.

2. **Initialize State from URL:** When the page loads, we check the URL to see which filters should be applied. This ensures that if we shares the URL or refreshes the page, the correct filtered list is shown.

By using the URL to store the current state, our app becomes more reliable and user-friendly. Users can bookmark or share specific views, and everything stays in sync, even after a page reload.

This helps to get rid of react states, reducing re-rendering dependency of React page. 

For example: 

