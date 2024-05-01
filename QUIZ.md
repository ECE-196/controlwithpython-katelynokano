### How does the DevBoard handle received serial messages? How does this differ from the naïve approach?

The DevBoard handles serial messaging by using interrupts, which is faster and more efficient than polling, where you constantly check for a change in value. The DevBoard only handles serial when it receives a change in serial, therefore freeing up time and resources.

### What does `detached_callback` do? What would happen if it wasn't used?
Detached threading allows the code to continue to process other things while awaiting a response from another section of the code, essentially allowing you to run parallel processing which is optimal for event-driven software like interrupts. If detached threading wasn't used, the code would have to wait on a response from one part of the code in order to run the next part, making it more susceptible to lag.

### What does `LockedSerial` do? Why is it _necessary_?
LockedSerial utilizes locking in order to ensure that the threading does not attempt to open up more than one serial port. This is necessary because you may be attempting to read/write over the same channel, which can cause the data to corrupt. This is why you cannot run the Python code in VSC while you have the serial monitor open on Arduino IDE.
