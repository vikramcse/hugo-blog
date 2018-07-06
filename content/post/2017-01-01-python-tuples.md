---
title: "Python: Tuple Fundamentals"
date: 2017-01-01
draft: false
tags: [Python]
---

Tuple represents one of the three currently implemented `sequence data types` along with `lists` and `ranges`.

Tuples are used to group any number of items into a single compound value regardless if their type

``` python
    >>> the_tuple = ('names', 55, False, 'youtube')
    >>> type (the_tuple)
    tuple
```

We can extract elements from the tuple using the index operator

``` python
    >>> the_tuple[1]
    55
```

The index must be a valid number and withing the range of the tuple

``` python
    >>> the_tuple[10]
    IndexError: tuple index out of range
```

We can perform also slicing like python lists.

``` python
    >>> the_tuple[1 : 3]
    (55, False)
```

We can use `in` operator in tuples

``` python
    >>> 55 in the_tuple
    True
```

keep in mind that tuples are immutable so trying to assing an iten is an error.

> `immutable` object is an object whose state cannot be modified after it is created.

``` python
    >>> the_tuple[1] = 'gmail'
    TypeError: 'tuple' object does not support item assignment
```

### Though tuples behavior is somewhat like python list but their are some constrains.

we can't add elements to a tuple. Tuples do not have `append` and `extend` methods

``` python
    >>> t.append("abcd")
	AttributeError: 'tuple' object has no attribute 'append'
```

we can not remove elements to a tuple. Tuples do not have `remove` and `pop` methods

``` python
    >>> t.remove("abcd")
	AttributeError: 'tuple' object has no attribute 'remove'
```

we can not find elements in a tuple. Tuples do not have `index` method.

``` python
    >>> t.index("abcd")
	AttributeError: 'tuple' object has no attribute 'index'
```

### So when we should use python tuple

* Tuples are faster than list, if you want to define some set of constant values and iterate it the use tuples instead list.

	for example: Suppose we want to define days in a week then we should use tuples instead list.

``` python
    >>> days_in_week = ('Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun')
```

- Tuples make your code safer as we can not modify the tuples (write protected), so no one add new day in the tuple
