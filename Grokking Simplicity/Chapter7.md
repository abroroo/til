
### Chapter 7 Deep copy when dealing with unknown source

This chapter focuses on maintaining the integrity of **copy-on-write (COW)** principles when integrating third-party or untrusted code. The challenge is that while our code may handle data immutably, external sources could still mutate this data, potentially affecting our system.

To address this, the chapter introduces **deep copying** (or defensive copying). This involves creating a deep copy of all nested data both when receiving input from third-party sources and when returning data. This ensures that any external mutations don't impact our immutable code.

![image](https://github.com/user-attachments/assets/e1d8b9dd-73c1-4fa4-ae38-458cc7b30e43)


However, deep copying is resource-intensive as it duplicates all data structures, unlike shallow copying, which only copies references. Therefore, use deep copying selectively, only when dealing with unknown sources or functions to safeguard your code’s immutability.

![image](https://github.com/user-attachments/assets/ab86d406-6dee-4885-9b5e-576e82fed953)


