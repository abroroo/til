# Chapter 17

In languages that have multiple threads, we would have to use
some kind of atomic update so that the threads could share mutable
state. However, we can take advantage of JavaScript’s single thread
and implement the primitive with a simple variable as long as we
access it synchronously. We’ll create a function. Every timeline
will call that function when it’s done. Every time the function is
called, we increment the number of times it has been called. Then,
when the last function calls it, it will call a callback:



## Example: 

<img width="400px" height="300px" src="https://github.com/user-attachments/assets/312ab674-0cd5-413f-9637-0e2fa7b3a296" />

### How It Works:
1. `Cut(2, function() { callback(total); })` creates a function (`done`) that tracks how many tasks (in this case, 2 tasks) need to complete before running the `callback`.
   
2. Every time `done()` is called, the counter (`num_finished`) inside `Cut()` is incremented. Once it reaches `2` (because we passed `2` as the first argument), the final callback is executed.

3. So, when `done()` is called after `cost_ajax` finishes, and `done()` is called again after `shipping_ajax` finishes, only **then** will the `callback(total)` be triggered.
