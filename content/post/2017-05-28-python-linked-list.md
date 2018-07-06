---
title: "Linked List implementation in Python"
date: 2017-05-28
draft: false
tags: [Python, Data Structure]
---

> In computer science Linked list is a data structure contains sequence of nodes where each node points to the next node in the sequence. We can also say the node stores a reference to the next node.

Linked List is a very popular data structure as it is very flexible and can be used to implement other abstract data types such as Stack, Queue, Tree and much more.

Let's first explore why we should use the Linked List.

### Advantages
1. New items can be added to the first and last to Linked List very easily
2. No need to define initial size of the Linked List
3. Backtracking can be implemented using Doubly where Linked List

### disadvantages
1. It takes more memory than to array to store the elements i.e. we need to store the reference of next node location
2. To access a elements form the Linked List we need to start form the head as it is a sequential access data structure, where in array we can access any element randomly

Ok vikram, that is enough theory knowledge, shall we start implementing the Linked List?

### Implementation

In Linked List the basic data block is a `Node` which holds two things
1. Data
2. Pointer to the next node

```python
class Node(object):
    """
    An internal class that represents a node with a single item
    and a link to the next node.
    """

    def __init__(self, item):
        self.item = item
        self.next = None
```

In the above code we created a class Node where the constructor accepts a data elements and initially the next pointer is None.

Now lets define Linked List class

```python
class LinkedList:
    def __init__(self):
        self.size = 0
        self.head = None
```

Here the constructor initializes the `size` which is initially `zero` and the `head` points to None. The `head` is used to store the first node location so that we can traverse to other nodes form head node.

Now it's time to add some element to Linked List, let's define append_last function.

```python
def append_last(self, value):
  if not value:
    return ValueError('Value must be need to insert into List')

    # Point 1
    new_node = Node(value)

    if self.head is None:
      self.head = new_node # Point 2
    else:
      # Point 3
      temp = self.head
      while temp.next is not None:
        temp = temp.next
      temp.next = new_node
  self.size += 1 # Point 4
```
Let's go through the append_last code, we are conforming that the inserting value is not None else we through exception.

Point 1: Here we are creating a new Node object with `value` as a data element and at this point the next pointer points to None

Point 2: If the List's as `head` variable is None means the List is empty so the newly created node is a `head` Node

Point 3: We come here when the `head` is not None, means the List has some elements, so the new Node is to be appended to the end Node. To access the end Node we need to traverse each node until we get next pointer None

Point 4: Increment the size if List

form above explanation we can notice the append_last Implementation was very easy, so why not to append at the front.

```python
def append_front(self, value):
  if not value:
    return ValueError('Value must be need to insert into stack')

    new_node = Node(value)

  if self.head is None:
      self.head = new_node
  else:
      new_node.next = self.head
      self.head = new_node
  self.size += 1
```

The `append_front` the explanation is same as `append_last` function the only difference is the new Node is to appended at the `front` so the new Node next pointer will point to the `head` Node and the `head` will be the `new` Node.

Here is full working code for Linked List

```python
class Node(object):
    """
    An internal class that represents a node with a single item
    and a link to the next node.
    """

    def __init__(self, item):
      self.item = item
      self.next = None


class LinkedList:
    def __init__(self):
      self.size = 0
      self.head = None

    def append_last(self, value):
      if not value:
        return ValueError('Value must be need to insert into List')

      new_node = Node(value)

      if self.head is None:
        self.head = new_node
      else:
        temp = self.head
        while temp.next is not None:
          temp = temp.next
        temp.next = new_node
    self.size += 1

    def append_front(self, value):
      if not value:
        return ValueError('Value must be need to insert into List')

      new_node = Node(value)

      if self.head is None:
        self.head = new_node
      else:
        new_node.next = self.head
        self.head = new_node
      self.size += 1

    def get_size(self):
      return self.size

    def __str__(self):
      temp = self.head
      ll_string = ''

      while temp is not None:
        ll_string += str(temp.item) + str(" ")
        temp = temp.next
      return ll_string.strip()
```
The Linked List is not always optimal choice of the data structure, there are other data structures those are better at some time.

### Time Analysis

|                            	| Linked List        	| Dynamic Array 	|
|----------------------------	|--------------------	|---------------	|
| Indexing                   	| O(n)               	| O(1)          	|
| Insert/delete at beginning 	| O(1)               	| O(n)          	|
| Insert/delete at end       	| O(1)               	| O(1)          	|
| Insert/delete in middle    	| Search Time + O(1) 	| O(n)          	|
| Wasted Space               	| O(n)               	| O(n)          	|

> One real life example of Liked List could be SMS messages, consider a multipart messages are received and each message has `next` pointer to the next consecutive message after receiving all the messages the messages are assembled by the next memory addresses
