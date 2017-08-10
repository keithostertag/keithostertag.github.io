---
layout: post
title: "Python- bytes, str, and unicode"
date: 2017-08-17
tags: python str unicode bytes
---

The following is taken from: "Effective Python: 59 Specific Ways to Write Better Python" by Brett Slatkin. I highly recommend this book.

> In Python 3, there are two types that represent sequences of characters: bytes and str. Instances of bytes contain raw 8-bit values. Instances of str contain Unicode characters.

> In Python 2, there are two types that represent sequences of characters: str and unicode. In contrast to Python 3, instances of str contain raw 8-bit values. Instances of unicode contain Unicode characters.

***

> You'll often need two helper functions to convert between these two cases and to ensure that the type of input values matches your code's expectations.

> In Python 3, you'll need one method that takes a str or bytes and always returns a str:

```
# Example 1 for python3
def to_bytes(bytes_or_str):
	if isinstance(bytes_or_str, str):
		value = bytes_or_str.encode('utf-8')
	else:
		value = bytes_or_str
	return value  # Instance of bytes
  ```

  > You'll need another method that takes a str or bytes and always returns a bytes:

  ```
  # Example 2 for python3
def to_bytes(bytes_or_str):
	if isinstance(bytes_or_str, str):
		value = bytes_or_str.encode('utf-8')
	else:
		value = bytes_or_str
	return value  # Instance of bytes
```
  > In Python 2, you'll need one method that takes a str or unicode and always returns a unicode:

  ```
  # Example 3 for python2
  def to_unicode(unicode_or_str):
	if isinstance(unicode_or_str, str):
		value = unicode_or_str.decode('utf-8')
	else:
		value = unicode_or_str
	return value  # Instance of unicode
  ```

  > You'll need another method that takes str or unicode and always returns a str:

  ```
  # example 4 for python2
def to_str(unicode_or_str):
	if isinstance(unicode_or_str, unicode):
		value = unicode_or_str.encode('utf-8')
	else:
		value = unicode_or_str
	return value  # Instance of str
  ```
