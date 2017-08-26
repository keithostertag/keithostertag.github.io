---
layout: post
title: "Python copy and intern"
date: 2017-08-25
tags: python copy intern memory
---

> "Assignment in Python _never_ copies values".

Sometimes it seems magical, like when you can swap values without using a third variable:

```python
>>> a = 5
>>> b = 88
>>> a,b = b,a
>>> a
88
>>> b
5
```

But sometimes it can catch you off-guard:

```python
>>> stuff = ['a','b','c']
>>> other_stuff = []
>>> for x in range(5):
...     other_stuff.append(stuff)
...
>>> other_stuff
[['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c']]
>>> other_stuff[1][1] = 'z'
>>> other_stuff
[['a', 'z', 'c'], ['a', 'z', 'c'], ['a', 'z', 'c'], ['a', 'z', 'c'], ['a', 'z', 'c']]
>>>

```

Let's check the memory id of each of the elements:
```python
>>> for x in other_stuff:
...     print(id(x))
...
140701071838856
140701071838856
140701071838856
140701071838856
140701071838856
>>>

```

Yep, all have the same memory id!

If we instead use copy:
```python
>>> import copy
>>> stuff = ['a','b','c']
>>> other_stuff = []
>>> for x in range(5):
...     other_stuff.append(copy.copy(stuff))
...
>>> other_stuff
[['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c']]
>>> for x in other_stuff:
...     print(id(x))
...
140098088041544
140098088077128
140098088075336
140098088077448
140098088110536
>>>
```

Now, each item in the other_stuff array has a unique memory address. So we now can do:

```python
>>> other_stuff[1][1] = 'z'
>>> other_stuff
[['a', 'b', 'c'], ['a', 'z', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c'], ['a', 'b', 'c']]
```

Here are a few links that helped me understand this better:

* [Subclassing Built-Ins, why are we using copy.copy ?](https://teamtreehouse.com/community/subclassing-builtins-why-are-we-using-copycopy)
* [python when to use copy.copy](https://stackoverflow.com/questions/7046971/python-when-to-use-copy-copy)
* [What does python sys.intern do, and when should it be used?](https://stackoverflow.com/questions/1136826/what-does-python-sys-intern-do-and-when-should-it-be-used)
* For a different example (creating a 10x10 matrix) see this: [Beware of object References!](https://www.reddit.com/r/pythontips/comments/4qgg95/beware_of_object_references/)
