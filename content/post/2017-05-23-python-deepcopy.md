---
title: "Python Copy and Deepcopy"
date: 2017-05-23
draft: false
tags: [Python]
---

## Python's Shallow and Deepcopy

Python's  integer, float, boolean, string and tuple are `immutable`, means once assigned value to a variable it's value can not be changed.

let's take a simple example

```python
number1 = 10
number2 = number1
```

In the above example as you can see we copied the reference of `number1` and assigned it to the `number2`. let's check if it is true!

```python
number1 = 10
print id(number1) # 54032216
number2 = number1
print id(number2) # 54032216
```

So let's re-assign the value of `number1 to 20`, then it should change the value of `number2` right? As the two variables are pointing to same location.

```python
number1 = 10
print id(number1) # 54032216
number2 = number1
print id(number2) # 54032216

number1 = 20

print number1 # 20
print number2 # 10 how?

print id(number1) # 54032333 <-- noticed?
print id(number2) # # 54032216
```

In this case when we assign the `number1` a different value so the variable `number1` got a new memory location as integers in python are `immutable`.

Now let's consider another type tuple which is also `immutable`.

``` python
address = (17, "street", 1222.22, 333.77)
address[1] = "india"

# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: 'tuple' object does not support item assignment
```

This means we can not mutate object as tuple in python are `immutable`.

> But here is a catch! what if the tuple contains mutable type values such as list, let's check

``` python
address = (17, "street", [1222.22, 333.77])
address[2].append(1000)
print address # address = (17, "street", [1222.22, 333.77])
```

We modified an element of the tuple `address`. This means the `immutability` of the tuple breaks if the tuple contains are `mutable`. The same is true for dictionary type as `dict` is also a mutable type object.

Now we know that the list is mutable so, let's check the behaviour of the list by example.

```python
items = [1, 2, 3]
print items # [1, 2, 3]

numbers = items
print numbers # [1, 2, 3]

print id(items) # 59972824
print id(numbers) # 59972824

items[2] = "python"
print items # [1, 2, 'python']
print numbers # [1, 2, 'python']

print id(items) # 59972900
print id(numbers) # 59972900
```
The two lists point to same location, and change in one list affect the another list, as the lists are mutable.

### Copying the python's mutable objects

We need to manually tell the python interpreter to stop mutating the object. This is done by the python's `copy` module.

##### Copying by slice operator
We can use the `slice` operator to copy an list and assign it to another.

```python
items = [1, 2, 3]
numbers = items[:]

print items # [1, 2, 3]
print numbers # [1, 2, 3]

print id(items) # 59579608
print id(numbers) # 5957928

numbers[2] = "python"

print items # [1, 2, 3]
print numbers # [1, 2, "python"]
```
By printing the memory location of two lists we can see that the lists are pointing to two different memory locations and change in one list has not affected the another list.

##### Copying by copy function

```python
from copy import copy
items = [1, 2, 3]
numbers = copy(items)

print items # [1, 2, 3]
print numbers # [1, 2, 3]

print id(items) # 52419600
print id(numbers) # 52465296

numbers[2] = "python"

print items # [1, 2, 3]
print numbers # [1, 2, "python"]
```

we achieved the same functionality by using `copy` (Shallow copy). The Shallow copy is mostly used to copy when the argument has a `compound` data structure such as list, dict etc.

##### Copying by deepcopy function

```python
from copy import copy
items = [1, 2, ["apple", "mango"]]
numbers = copy(items)

print items # [1, 2, ["apple", "mango"]]
print numbers # [1, 2, ["apple", "mango"]]

print id(items) # 52419600
print id(numbers) # 52465296

numbers[2][1] = "pineapple"

print items # [1, 2, ["apple", "pineapple"]]
print numbers # [1, 2, ["apple", "pineapple"]]
```

The list defined inside list are not copied as the reference is shared between the two lists, therefore change in one sub list affected another.
To stop this behavior there is `deepcopy` function inside copy module of python.

```python
from copy import deepcopy
items = [1, 2, ["apple", "mango"]]
numbers = deepcopy(items)

print items # [1, 2, ["apple", "mango"]]
print numbers # [1, 2, ["apple", "mango"]]

print id(items) # 52419600
print id(numbers) # 52465296

numbers[2][1] = "pineapple"

print items # [1, 2, ["apple", "mango"]]
print numbers # [1, 2, ["apple", "pineapple"]]
```

After using the `deepcopy` we can see the change in the `numbers` list is not reflected into another list.

### Why to use copy and deepcopy?
- In the `distributed environment` where there is a possibility of `race condition` where two or more connections can access same list and make changes to it and this will introduce unexpected behavior.

- Is easier to `read`, easier to `maintain` and less likely to have `unpredictable` result.
