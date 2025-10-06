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
  ### [Task A] ----notify----> [Task B]
- Only passes an integer/flag
- Super fast (no buffer)
- One-to-one
-  Example Use: Task A signals Task B that "data ready"
## Message Queue
### Definition:
- Tasks communicate by sending messages into a FIFO queue.
- Use Case: Sharing structured data, buffering sensor values, producer-consumer model.
- Pros: Stores multiple messages, ordered communication.
- Cons: Needs memory for queue buffer.
  ### [Producer Task] ---> [ Queue Buffer (FIFO) ] ---> [Consumer Task]
- Multiple messages stored (FIFO order)
- Safe for producer-consumer
- One-to-one or one-to-many
- Example Use: Sensor data producer → Logger consumer
## Pipe
### Definition:
- A unidirectional communication channel between processes. Data written at one end is read at the other.
- Use Case: Process-to-process communication in Linux (ls | grep).
- Pros: Simple, stream-based, supported by OS.
- Cons: Only unidirectional, byte stream (not structured messages).
  ###  [Process A] --write--> [   | Kernel Pipe |   ] --read--> [Process B]
- Unidirectional stream of bytes
- Used between parent-child processes
- OS-managed
- Example Use: "ls | grep txt" in Linux shell
## Mailbox
### Definition:
- A special structure that holds one message at a time, often used in RTOS.
- Use Case: When tasks exchange single messages/events (like a mailbox).
- Pros: Direct task-to-task communication with message payload.
- Cons: Limited storage (often 1-slot).
  ### [Task A] ---> [ Mailbox (1 slot) ] ---> [Task B]
- Holds only ONE message at a time
- Light-weight
- Overwrites or blocks if full
- Example Use: Command/control messages in RTOS
