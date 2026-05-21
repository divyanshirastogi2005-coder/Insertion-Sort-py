#Circular Queue,
class CircularQueue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.queue = [None] * capacity
        self.front = -1
        self.rear = -1

    def enqueue(self, item):
        # Overflow Condition: (rear + 1) % capacity == front
        if (self.rear + 1) % self.capacity == self.front:
            print("Queue Overflow! Cannot enqueue:", item)
            return False
            
        # First element insertion sequence
        if self.front == -1:
            self.front = 0
            
        # Modulo arithmetic increment for wrap-around
        self.rear = (self.rear + 1) % self.capacity
        self.queue[self.rear] = item
        return True

    def dequeue(self):
        # Underflow Condition: front == -1
        if self.front == -1:
            print("Queue Underflow! The queue is empty.")
            return None
            
        removed_item = self.queue[self.front]
        self.queue[self.front] = None  # Clear slot
        
        # Scenario: Queue becomes completely empty after this operation
        if self.front == self.rear:
            self.front = -1
            self.rear = -1
        else:
            # Modulo arithmetic increment for wrap-around
            self.front = (self.front + 1) % self.capacity
            
        return removed_item

# Testing the Circular Queue
cq = CircularQueue(3)
cq.enqueue(5)
cq.enqueue(10)
cq.enqueue(15)
cq.enqueue(20)  # Should trigger overflow

print("Dequeued:", cq.dequeue())
cq.enqueue(25)  # Should work because slot wrapped around
print("Queue State:", cq.queue)

