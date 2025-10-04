# SEMOPHORES
- A semaphore is a synchronization mechanism used to control access to a shared resource by multiple threads or processes in a concurrent system.
- It uses an integer counter that is modified atomically using two main operations:
  - wait() / P() / sem_wait() → Decrement (lock / acquire resource)
  - signal() / V() / sem_post() → Increment (unlock / release resource)
### Real-World Example
- Printer Access: If 3 printers are available, up to 3 users can print simultaneously. When all are busy, new requests wait.
- Critical Section Protection: Only one thread should update a shared variable at a time.
## Types of Semaphores
### Binary Semaphore
#### Definition:
- A semaphore with only two values: 0 or 1 (locked/unlocked).
#### Explanation:
- It is used as a simple lock mechanism (similar to a mutex). Only one thread can access the resource at a time.
#### Use Case:
- Protect a critical section where only one task can run at a time.
```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
sem_t bin_sem; // binary semaphore
void* task(void* arg) {
    sem_wait(&bin_sem); // acquire semaphore
    printf("Thread %ld is in critical section\n", (long)arg);
    sleep(1); // simulate work
    printf("Thread %ld leaving critical section\n", (long)arg);
    sem_post(&bin_sem); // release semaphore
    return NULL;
}
int main() {
    pthread_t t1, t2;
    sem_init(&bin_sem, 0, 1); // binary semaphore initialized to 1
    pthread_create(&t1, NULL, task, (void*)1);
    pthread_create(&t2, NULL, task, (void*)2);
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    sem_destroy(&bin_sem);
    return 0;
}
```
### Counting Semaphore
#### Definition:
- A semaphore that allows a count > 1, representing multiple available resources.
#### Explanation:
- Instead of allowing only one thread, it allows N threads to access a resource at the same time (until count reaches 0).
#### Use Case:
- Control access to a pool of resources (e.g., connection pool, limited hardware devices).
```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
sem_t count_sem; // counting semaphore
void* task(void* arg) {
    sem_wait(&count_sem); // acquire one slot
    printf("Thread %ld acquired resource\n", (long)arg);
    sleep(2); // simulate work
    printf("Thread %ld releasing resource\n", (long)arg);
    sem_post(&count_sem); // release slot
    return NULL;
}
int main() {
    pthread_t t[5];
    sem_init(&count_sem, 0, 3); // allow up to 3 threads at a time
    for (long i = 0; i < 5; i++)
        pthread_create(&t[i], NULL, task, (void*)i+1);
    for (int i = 0; i < 5; i++)
        pthread_join(t[i], NULL);
    sem_destroy(&count_sem);
    return 0;
}
```
### Mutex (Mutual Exclusion Lock)
#### Definition:
- A mutex is a locking mechanism that allows only one thread to access a critical section.
#### Difference from Binary Semaphore:
- Mutex has ownership — the thread that locks it must be the one to unlock it.
#### Use Case:
- When you want strict ownership and prevent accidental unlocking by other threads.
```c
#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
pthread_mutex_t lock;
void* task(void* arg) {
    pthread_mutex_lock(&lock); // acquire lock
    printf("Thread %ld is in critical section\n", (long)arg);
    sleep(1);
    printf("Thread %ld leaving critical section\n", (long)arg);
    pthread_mutex_unlock(&lock); // release lock
    return NULL;
}
int main() {
    pthread_t t1, t2;
    pthread_mutex_init(&lock, NULL);
    pthread_create(&t1, NULL, task, (void*)1);
    pthread_create(&t2, NULL, task, (void*)2);
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    pthread_mutex_destroy(&lock);
    return 0;
}
```
![Uploading image.png…]()
