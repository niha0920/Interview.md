# IPC Mechanisms (Inter-Process / Inter-Task Communication)
- IPC allows processes or tasks to exchange data and synchronize execution when running concurrently.
## Types
- Direct Task Notification
- Message Queues
- Pipes
- Mailbox
## Direct Task Notification
### Definition:
- A lightweight signaling mechanism where one task directly notifies another. (Used in FreeRTOS, RTOS kernels, etc.)
- Use Case: Event signaling, simple synchronization, incrementing counters.
- Pros: Fast, lightweight (no memory buffer).
- Cons: Only for signal/flags, not for large data.
