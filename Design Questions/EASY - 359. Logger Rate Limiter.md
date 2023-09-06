Design a logger system that receives a stream of messages along with their timestamps. 
Each unique message should only be printed at most every 10 seconds (i.e. a message printed at timestamp t will prevent other identical messages from being printed 
until timestamp t + 10).

All messages will come in chronological order. Several messages may arrive at the same timestamp.

Implement the Logger class:

* Logger() Initializes the logger object.
* bool shouldPrintMessage(int timestamp, string message) Returns true if the message should be printed in the given timestamp, otherwise returns false.
_________________________________________________________________________________________________________________________

### Understanding of the Question :

* First we need to initialize a logger object
* Then, we are going to receive messages and their timestamps as input.
* We need to update them to the logger based on some conditions.
* Condition - Next identical message should be printed only at t+10, or else return False
______________________________________________________________________________________________________________________________

### We are given with this code with two functions

```python
class Logger:
    def __init__(self):
        
    def shouldPrintMessage(self, timestamp: int, message: str) -> bool:
        
# Your Logger object will be instantiated and called as such:
# obj = Logger()
# param_1 = obj.shouldPrintMessage(timestamp,message)
```
__________________________________________________________________________________________________________________

#### Solution and Source Code:

* This code defines a Python class called Logger that is used to log and control the printing of messages based on timestamps.
* Initialize an empty dictionary called self.logger to store messages and their corresponding timestamps.
* shouldPrintMessage(self, timestamp: int, message: str) -> bool: This is the main method of the class. It takes two arguments: timestamp, which is an integer
  representing the current time when a message is logged, and message, which is a string representing the message to be logged.

Now inside the print message function, we are going to check two conditions:

IF PART:

* If the message is not in the dictionary, it means this message is being logged for the first time.
* so it adds the message to the dictionary with its corresponding timestamp and returns True to indicate that the message should be printed.

ELSE PART:

* If the message is already present in the dictionary, it means this message has been logged before.
* In this case, it checks if the time difference between the current timestamp and the previously logged timestamp for the same message
  (stored in self.logger[message]) is less than 10 units of time.
* If the time difference is less than 10 units, it returns False to indicate that the message should not be printed because it's considered a duplicate or too frequent.
* If the time difference is greater than or equal to 10 units, it updates the timestamp in the dictionary to the current timestamp and returns True.
* This indicates that the message can be printed now because there has been a sufficient time gap since the last time it was logged.

```python
class Logger:
    def __init__(self):
        self.logger = {}
    
    def shouldPrintMessage(self, timestamp: int, message: str) -> bool:
        if message not in self.logger:
            self.logger[message] = timestamp
            return True
        else:
            if timestamp < self.logger[message]+10:
                return False
            else:
                self.logger[message] = timestamp
                return True
```


Time Complexity: O(1). The lookup and update of the hashtable takes a constant time.

Space Complexity: O(M) where M is the size of all incoming messages. Over time, the hashtable would have an entry for each unique message that has appeared.




