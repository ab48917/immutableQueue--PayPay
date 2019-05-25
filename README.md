# immutableQueue--PayPay
This repository has immutableQueue implementations which is implemented by two immutable Stacks.

# Immutable Queue
Implements interface Queue.

Represented by class ImmutableQueue.
 
1- The philosophy is that since a queue is effectively a reverse stack, it can be implemented using 2 stacks.

2- Has 2 immutable stacks, backwards and forwards, to keep track of the items being enQueued and deQueued, respectively.

3- No public constructor. Forced to start with an empty queue, which is a singleton represented by inner class EmptyQueue.

4- Has a reverse() utility method that is used to reverse a stack. Runs in O(n) time.

5- Has a private constructor which builds itself using the backwards and forwards stacks provided as parameters.

6- enQueue() operation just pushes the new item to the backwards and creates a new queue using the existing forwards stack and the new backwards stack. There is one exception to this, however, when the very first enQueue is done (on the EmptyQueue). In that case, the item is pushed to the forwards stack. This is necessary since otherwise deQueue() will always fail, as per the deQueue logic described below. Runs in O(1) time.

7- deQueue() operation is a bit tricky. It first pops from the forwards stack. Now it can have a few cases:

  7.1- If the resulting stack of the pop() operation is the not the empty stack (means there are still items on the forwards stack to be deQueued), it returns a new queue constructed with the resulting stack as forwards and the existing backwards as backwards.
  7.2- If the resulting stack of the pop() operation is the empty stack (means there are no more items on the forwards stack to be deQueued), there could be two further sub-cases:
  7.3- If the backwards stack is empty as well, then what we have at this point is an empty queue. So it just returns the empty singleton queue.
  7.4- If the backwards stack is not empty, however, then we need to get rid of the bottommost item in the backwards stack. This is accomplished by reversing the backwards stack (using the rerverse() method). Finally, it returns a new queue constructed using the reversed stack as forwards and the empty singleton stack as backwards.
  7.5- The last case is the worst case where the runtime of deQueue() is O(n). All the previous cases are O(1).

8- head() operation just returns the head of the forwards stack. Runs in O(1) time.

9- IsEmpty() is always true for the empty singleton queue. Otherwise it's always false. Runs in O(1) time.

Question 2- Design a backend systems to behave like google analytics.
1-  Please review the design diagram. It has necessary notes for special mentions in case of huge data processing.
2-  I have considered few assumations regarding Database selections [considered NOSQL -MONGO DB] 
    and Micro services architecture for backend architecture.
3-  Used JS scripts to inject to client browser as part of cookie and run in client machine to retrieve the user's info.
4-  Pass the Users info to Micro service using POST call. [Can use CQRS as well to move the data in case POST doe not serve well].
5- Considerd that It's gonna be very frequent call hence use POST than emitting very frequent events may cause listener latancy.
6- Once service receives the data, It is going to store as seperate document in users collection. Appending all the user page surfings may cause huge document size.
7- It is suggested to have millions of documents in a collection of smaller size than holding few documents of heavy size, Heavey size documents impacts RAM to read and process and hence retrieve slows down.
8- Anytime, It can either be fetched by a get call\or event to view service and let application do parallel processing using STREAM or ParallelStream.
9- Construct the UI compaitable payload and let it get rendered by application UI code in your browser.

 
