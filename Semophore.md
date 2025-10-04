# SEMOPHORES
- A semaphore is a synchronization mechanism used to control access to a shared resource by multiple threads or processes in a concurrent system.
- It uses an integer counter that is modified atomically using two main operations:
  - wait() / P() / sem_wait() → Decrement (lock / acquire resource)
  - signal() / V() / sem_post() → Increment (unlock / release resource)
#### Real-World Example
- Printer Access: If 3 printers are available, up to 3 users can print simultaneously. When all are busy, new requests wait.
- Critical Section Protection: Only one thread should update a shared variable at a time.
### Types of Semaphores
### Binary Semaphore
##### Definition:
A semaphore with only two values: 0 or 1 (locked/unlocked).
##### Explanation:
It is used as a simple lock mechanism (similar to a mutex). Only one thread can access the resource at a time.
###### Use Case:
Protect a critical section where only one task can run at a time.
