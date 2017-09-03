---
layout: post
title: "Python regex lookaround"
date: 2017-09-03
tags: python regex
---

An online exercise that I ran into asks:
> Create a program asking the user to enter a new password and check that the submitted password should contain at least one number, one uppercase letter and at least 5 characters. If the conditions are generated, print out "OK, password is fine", otherwise print "Sorry, password does not meet criteria" and continues to prompt.

Here is the given solution:
```python
while True:
    psw = input("Enter new password: ")
    if any(i.isdigit() for i in psw) and any(i.isupper() for i in psw) and len(psw) >= 5:
        print("OK, password is fine")
        break
    else:
        print("Sorry, password does not meet criteria")
```

OK, that works. But I wanted to solve the problem using regex.  

I must admit... I could not solve it on my own, as my familiarity with regex is still pretty basic.  

So I decided to ask for help on my local slack community, and Leslie Heinzen (aka zero-man) came to my rescue. Here is my solution using his regex:

```python
import re

def pw():
    """Password criteria: at least one upper case letter and one digit, total of at least 5 characters.
    """
    while True:
        password = input("Enter password: ")
        permit = re.compile(r'(?=.*[A-Z])(?=.*[0-9])[a-zA-Z0-9]{5,}')
        if permit.search(password):
            print("OK, password is fine")
            break
        else:
            print("Sorry, password doesn't meet criteria")

pw()
```
The last character set `[a-zA-Z0-9]` can be easily modified to include any other characters that I would want to allow.

Lookaround is a regex feature that I had not looked at before. I'm still studying it, but here are a few links that I have found very helpful:
* [regular expressions 101](https://regex101.com/)
* [Regular Expressions Tutorial](http://www.regular-expressions.info/tutorial.html)
* [Lookahead and Lookbehind Zero-Length Assertions](http://www.regular-expressions.info/lookaround.html)
