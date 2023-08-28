Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

1. void push(int x) Pushes element x to the top of the stack.
2. int pop() Removes the element on the top of the stack and returns it.
3. int top() Returns the element on the top of the stack.
4. boolean empty() Returns true if the stack is empty, false otherwise.

Notes:

-- You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.

-- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use 
   only a queue's standard operations.

Input

["MyStack", "push", "push", "top", "pop", "empty"]

[[], [1], [2], [], [], []]

Output:

[null, null, null, 2, 2, false]

Explanation

MyStack myStack = new MyStack();

myStack.push(1);

myStack.push(2);

myStack.top(); // return 2

myStack.pop(); // return 2

myStack.empty(); // return False

Follow-up: Can you implement the stack using only one queue?
_________________________________________________________________________________________________

#### What do we know about stack?

1. Stack is a LIFO (last in - first out) data structure, in which elements are added and removed from the same end, called top.
2. In general stack is implemented using an array or linked list.
3. But in this particular question, we will review a different approach for implementing stack using queues.

#### What do we know about Queue?

1. In contrast queue is a FIFO (first in - first out) data structure, in which elements are added only from the one side - rear
   and removed from the other - front.
2. In the question they have asked us to implement a stack using two queues, which will not give us an optimized solution.
3. So we are going to implement a stack using one queue.
__________________________________________________________________________________________________________

#### Solution:

Time complexity : O(1)
Space complexity : O(1)

1. Initialize a double-ended queue (deque).
2. push(self, x: int) -> None: This method is used to push (add) an element x onto the stack. It simply appends the given value to the
   the right side of the deque using the append() method.
3. top(self) -> int: This method returns the top element of the stack without actually removing it. It accesses the rightmost (last) element
   of the deque using the index [-1].
4. empty(self) -> bool: This method checks if the stack is empty. If the length of the deque is 0, it means the stack is empty, so it returns
   True; otherwise, it returns False.

Pop: 
1. pop(self) -> int: This method is used to pop (remove) an element from the stack.
2. It simulates the process of removing the top element of the stack by re-enqueueing all elements except the last one.
3.  It iterates through the elements of the deque except the last one and uses the popleft() method to remove them from the left side
4.  and then immediately pushes them back onto the stack using the push() method.
5.  After re-enqueuing all elements except the last one, it then removes and returns the last element, which effectively simulates popping
    from the top of the stack.

In summary, the below code implements a stack data structure using a double-ended queue. The push() and top() methods are straightforward, but the 
pop() method uses a creative approach to simulate the removal of elements from the top of the stack by temporarily re-enqueuing elements.

```python
class MyStack:

    def __init__(self):
        #Initialize a double-ended queue
        self.q = deque()

    def push(self, x: int) -> None:
        #Append value to the right side of the queue
        self.q.append(x)
        
    def pop(self) -> int:
        #Pop every value except the last one
        for i in range(len(self.q)-1):
            self.push(self.q.popleft())
        return self.q.popleft()
        
    def top(self) -> int:
        #Return the top most element- rightmost value of queue
        return self.q[-1]

    def empty(self) -> bool:
        if len(self.q) == 0: return True
        return False
```

 
