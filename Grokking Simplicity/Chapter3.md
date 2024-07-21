## Chapter 3

### How to Detect a Calculation from an Action

To figure out if something is a calculation or an action, think about decision-making. If there's a decision being made, it's a calculation. When you do something based on that calculation, that's an action.


![image](https://github.com/user-attachments/assets/0418bdca-68dd-43ae-a006-a4e206d6f8f3)

**Example: Breaking Down `sendEmail()`**

- **Email Address = DATA**: The raw information you need.
- **Determine Where to Send the Email = CALCULATION**: Deciding the email address to use.
- **Send the Email = ACTION**: Actually sending the email.

When you look at code, it might seem like everything is an action. To spot calculations, ask yourself: "What's making a decision here?"

![image](https://github.com/user-attachments/assets/71c7ebc2-ce46-4d43-9af4-fec2803b351b)

### What are Actions?

Even just accessing a variable can be an action. For example, if you access `y`, depending on where `y` is (outer scope or inner scope), it can change the function's output. So, actions are any operations that can vary based on when or how they're performed.

![image](https://github.com/user-attachments/assets/585e4137-2a70-45fd-b9f1-29091111f8c9)
