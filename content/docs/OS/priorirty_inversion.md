---
title: Priority Inversion
BookToC: true
---
# Priority Inversion

## Example of a priority inversion

Consider two tasks H and L, of high and low priority respectively, either of which can acquire exclusive use of a shared resource R. If H attempts to acquire R after L has acquired it, then H becomes blocked until L relinquishes the resource. Sharing an exclusive-use resource (R in this case) in a well-designed system typically involves L relinquishing R promptly so that H (a higher priority task) does not stay blocked for excessive periods of time. 

Despite good design, however, it is possible that a third task M of medium priority (p(L) < p(M) < p(H), where p(x) represents the priority for task (x)) becomes runnable during L's use of R. At this point, M being higher in priority than L, preempts L (since M does not depend on R), causing L to not be able to relinquish R promptly, in turn causing H—the highest priority process—to be unable to run (that is, H suffers unexpected blockage indirectly caused by lower priority tasks like M).

## Solutions

### Disabling all interrupts to protect critical sections
When disabling interrupts is used to prevent priority inversion, there are only two priorities: preemptible, and interrupts disabled. With no third priority, inversion is impossible. Since there's only one piece of lock data (the interrupt-enable bit), misordering locking is impossible, and so deadlocks cannot occur. Since the critical regions always run to completion, hangs do not occur. Note that this only works if all interrupts are disabled. If only a particular hardware device's interrupt is disabled, priority inversion is reintroduced by the hardware's prioritization of interrupts. In early versions of UNIX, a series of primitives named splx(0) ... splx(7) disabled all interrupts up through the given priority. By properly choosing the highest priority of any interrupt that ever entered the critical section, the priority inversion problem could be solved without locking out all of the interrupts. Ceilings were assigned in rate-monotonic order, i.e. the slower devices had lower priorities.
In multiple CPU systems, a simple variation, "single shared-flag locking" is used. This scheme provides a single flag in shared memory that is used by all CPUs to lock all inter-processor critical sections with a busy-wait. Interprocessor communications are expensive and slow on most multiple CPU systems. Therefore, most such systems are designed to minimize shared resources. As a result, this scheme actually works well on many practical systems. These methods are widely used in simple embedded systems, where they are prized for their reliability, simplicity and low resource use. These schemes also require clever programming to keep the critical sections very brief. Many software engineers consider them impractical in general-purpose computers.[citation needed]

### Priority ceiling protocol
With priority ceiling protocol, the shared mutex process (that runs the operating system code) has a characteristic (high) priority of its own, which is assigned to the task locking the mutex. This works well, provided the other high priority task(s) that tries to access the mutex does not have a priority higher than the ceiling priority.

### Priority inheritance
Under the policy of priority inheritance, whenever a high priority task has to wait for some resource shared with an executing low priority task, the low priority task is temporarily assigned the priority of the highest waiting priority task for the duration of its own use of the shared resource, thus keeping medium priority tasks from pre-empting the (originally) low priority task, and thereby affecting the waiting high priority task as well. Once the resource is released, the low priority task continues at its original priority level.

### Random boosting
Ready tasks holding locks are randomly boosted in priority until they exit the critical section. This solution is used in Microsoft Windows.

### Avoid blocking
Because priority inversion involves a low-priority task blocking a high-priority task, one way to avoid priority inversion is to avoid blocking, for example by using non-blocking synchronization or read-copy-update.