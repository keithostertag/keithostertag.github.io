---
layout: post
title: "Python recursive generator example"
date: 2017-08-24
tags: python generator str lists
---

The following is taken from "Beginning Python", 3rd edition, 2017 by Magnus Lie Hetland.

The goal of this example is to flatten a series of arbitrarily deep nested lists using a recursive generator.

```python
def flatten(nested):
    try:
        #Don't iterate over string-like objects:
        try:
            nested + " "
        except TypeError:
                pass
        else:
            raise TypeError
        for sublist in nested:
            for element in flatten(sublist):
                yield element

    except TypeError:
        yield nested

print(list(flatten(['foo',1,2,3, ('2','3'),['bar','123',['baz']]])))
```
The output is `['foo', 1, 2, 3, '2', '3', 'bar', '123', 'baz']`

In this case, we don't want to iterate over string-like objects; we want to treat them as atomic values, not sequences that should be flattened.

To test if an object is string-like, this code `try`'s to concatenate it with a string (" "). If the expression `nested + " "` raises a `TypeError`, it is ignored; however, if the expression does _not_ raise the `TypeError`, the `else` clause of the inner `try` statement raises a `TypeError` of its own. This causes the string-like object to be yielded _as is_ (in the outer `except` clause).

This is one of the few times I've seen a `pass` statement used with purpose in a working code sample, Hah!

Here's the same function rewritten as a plain function (without a generator):

```python
def flatten(nested):
    result = []
    try:
        #Don't iterate over string-like objects:
        try:
            nested + " "
        except TypeError:
                pass
        else:
            raise TypeError
        for sublist in nested:
            for element in flatten(sublist):
                result.append(element)

    except TypeError:
        result.append(nested)
    return nested

```
