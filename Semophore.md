## SEMOPHORES
- A semaphore is a synchronization mechanism used to control access to a shared resource by multiple threads or processes in a concurrent system.
- It uses an integer counter that is modified atomically using two main operations:
  - wait() / P() / sem_wait() → Decrement (lock / acquire resource)
  - signal() / V() / sem_post() → Increment (unlock / release resource)

