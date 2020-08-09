---
title: Mutex, semaphore
BookToC: true
---
# Mutex, semaphore

critical section.

mutual exclusion, that is, some way of making sure that if one process is using a shared variable or file, the other processes will be excluded from doing the same thing.

mutual exclusion with busy waiting, options:
- disabling interrupts: software should not do this
- lock variables: use lock 0/1. has fatal flaw - two processes could see lock is 0 and try to lock it at the same time.
- strict alternation: low effectiveness
- Peterson's solution: will work, but will "busy waiting"
- TSL: test and set lock. will work, but "busy waiting"

Peterson's solution and TSL both will work, but busy waiting might leads to unexpected issue: priority inversion.

sleep and awake

semaphore:

Checking the value, changing it, and possibly going to sleep, are all done as a single, indivisible atomic action.



### Locks
Lock: an object that can only be owned by a single thread at any given time. Basic operations on a lock:
acquire: mark the lock as owned by the current thread; if some other thread already owns the lock then first wait until the lock is free. Lock typically includes a queue to keep track of multiple waiting threads.
release: mark the lock as free (it must currently be owned by the calling thread).
Too much milk solution with locks (using Pintos APIs):
```c++
struct lock l;
...
lock_acquire(&l);
if (milk == 0) {
  buy_milk();
}
lock_release(&l);
```

A more complex example: producer/consumer.

Producers add characters to a buffer
Consumers remove characters from the buffer
Characters will be removed in the same order added

Version 1:
```c++
char buffer[SIZE];
int count = 0, putIndex = 0, getIndex = 0;
struct lock l;
lock_init(&l);

void put(char c) {
    lock_acquire(&l);
    count++;
    buffer[putIndex] = c;
    putIndex++;
    if (putIndex == SIZE) {
        putIndex = 0;
    }
    lock_release(&l);
}

char get() {
    char c;
    lock_acquire(&l);
    count--;
    c = buffer[getIndex];
    getIndex++;
    if (getIndex == SIZE) {
        getIndex = 0;
    }
    lock_release(&l);
    return c;
}
```

Version 2 (handle empty/full cases):
```c++
char buffer[SIZE];
int count = 0, putIndex = 0, getIndex = 0;
struct lock l;
lock_init(&l);

void put(char c) {
    lock_acquire(&l);
    while (count == SIZE) {
        lock_release(&l);
        lock_acquire(&l);
    }
    count++;
    buffer[putIndex] = c;
    putIndex++;
    if (putIndex == SIZE) {
        putIndex = 0;
    }
    lock_release(&l);
}

char get() {
    char c;
    lock_acquire(&l);
    while (count == 0) {
        lock_release(&l);
        lock_acquire(&l);
    }
    count--;
    c = buffer[getIndex];
    getIndex++;
    if (getIndex == SIZE) {
        getIndex = 0;
    }
    lock_release(&l);
    return c;
}
```

### Condition Variables

From[link](https://en.cppreference.com/w/cpp/thread/condition_variable)

The condition_variable class is a synchronization primitive that can be used to block a thread, or multiple threads at the same time, until another thread both modifies a shared variable (the condition), and notifies the condition_variable.

The thread that intends to modify the variable has to

1. acquire a `std::mutex` (typically via `std::lock_guard`)
2. perform the modification while the lock is held
3. execute notify_one or notify_all on the `std::condition_variable` (the lock does not need to be held for notification)

Even if the shared variable is atomic, it must be modified under the mutex in order to correctly publish the modification to the waiting thread.

Any thread that intends to wait on `std::condition_variable` has to

acquire a `std::unique_lock<std::mutex>`, on the same mutex as used to protect the shared variable

either
1. check the condition, in case it was already updated and notified
2. execute wait, wait_for, or wait_until. The wait operations atomically release the mutex and suspend the execution of the thread.
3. When the condition variable is notified, a timeout expires, or a [*spurious wakeup*](https://en.wikipedia.org/wiki/Spurious_wakeup) occurs, the thread is awakened, and the mutex is atomically reacquired. The thread should then check the condition and resume waiting if the wake up was spurious.

or

use the predicated overload of wait, wait_for, and wait_until, which takes care of the three steps above
std::condition_variable works only with `std::unique_lock<std::mutex>`; this restriction allows for maximal efficiency on some platforms. std::condition_variable_any provides a condition variable that works with any BasicLockable object, such as `std::shared_lock`.

Condition variables permit concurrent invocation of the wait, wait_for, wait_until, notify_one and notify_all member functions.

```c++
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
#include <condition_variable>
 
std::mutex m;
std::condition_variable cv;
std::string data;
bool ready = false;
bool processed = false;
 
void worker_thread()
{
    // Wait until main() sends data
    std::unique_lock<std::mutex> lk(m);
    cv.wait(lk, []{return ready;});
 
    // after the wait, we own the lock.
    std::cout << "Worker thread is processing data\n";
    data += " after processing";
 
    // Send data back to main()
    processed = true;
    std::cout << "Worker thread signals data processing completed\n";
 
    // Manual unlocking is done before notifying, to avoid waking up
    // the waiting thread only to block again (see notify_one for details)
    lk.unlock();
    cv.notify_one();
}
 
int main()
{
    std::thread worker(worker_thread);
 
    data = "Example data";
    // send data to the worker thread
    {
        std::lock_guard<std::mutex> lk(m);
        ready = true;
        std::cout << "main() signals data ready for processing\n";
    }
    cv.notify_one();
 
    // wait for the worker
    {
        std::unique_lock<std::mutex> lk(m);
        cv.wait(lk, []{return processed;});
    }
    std::cout << "Back in main(), data = " << data << '\n';
 
    worker.join();
}
```
=====
The class std::condition_variable is a StandardLayoutType. It is not CopyConstructible, MoveConstructible, CopyAssignable, or MoveAssignable.

Synchronization mechanisms need more than just mutual exclusion; also need a way to wait for another thread to do something (e.g., wait for a character to be added to the buffer)

Condition variables: used to wait for a particular condition to become true (e.g. characters in buffer).

wait(condition, lock): release lock, put thread to sleep until condition is signaled; when thread wakes up again, re-acquire lock before returning.

signal(condition, lock): if any threads are waiting on condition, wake up one of them. Caller must hold lock, which must be the same as the lock used in the wait call.

broadcast(condition, lock): same as signal, except wake up all waiting threads.

Note: after signal, signaling thread keeps lock, waking thread goes on the queue waiting for the lock.
Warning: when a thread wakes up after cond_wait there is no guarantee that the desired condition still exists: another thread might have snuck in.

Producer/Consumer, version 3 (with condition variables):
```c++
char buffer[SIZE];
int count = 0, putIndex = 0, getIndex = 0;
struct lock l;
struct condition dataAvailable;
struct condition spaceAvailable;

lock_init(&l);
cond_init(&dataAvailable);
cond_init(&spaceAvailable);

void put(char c) {
    lock_acquire(&l);
    while (count == SIZE) {
        cond_wait(&spaceAvailable, &l);
    }
    count++;
    buffer[putIndex] = c;
    putIndex++;
    if (putIndex == SIZE) {
        putIndex = 0;
    }
    cond_signal(&dataAvailable, &l);
    lock_release(&l);
}

char get() {
    char c;
    lock_acquire(&l);
    while (count == 0) {
        cond_wait(&dataAvailable, &l);
    }
    count--;
    c = buffer[getIndex];
    getIndex++;
    if (getIndex == SIZE) {
        getIndex = 0;
    }
    cond_signal(&spaceAvailable, &l);
    lock_release(&l);
    return c;
}
```

### Monitors
When locks and condition variables are used together like this, the result is called a monitor :

A collection of procedures manipulating a shared data structure.
One lock that must be held whenever accessing the shared data (typically each procedure acquires the lock at the very beginning and releases the lock before returning).
One or more condition variables used for waiting.
There are other synchronization mechanisms besides locks and condition variables. Be sure to read about semaphores in the book or in the Pintos documentation.