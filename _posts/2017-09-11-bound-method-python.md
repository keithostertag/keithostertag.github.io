---
layout: post
title: "Creative example using a bound method in Python"
date: 2017-09-11
tags: python str max bound
---

I found this code challenge on checkio.org, but the really interesting thing to me are the solutions which show unique and educational approaches.  

The code challenge was this:  

```
You are given a text which only contains ASCII symbols.

(a)You should find the most frequent letter in the text. The letter returned must be in lower case.
Ignore all other characters such as digits, punctuation and whitespace.

(b)If you have two or more letters with the same highest frequency,
then return the letter which comes first in the latin alphabet.
For example -- "one" contains "o", "n", "e" only once for each, thus we choose "e".

input: text, output: most frequent letter in text
```

My solution, and many others, took about 10-12 lines of code. Checkio user **veky**'s solution uses only two!  

Here's his solution:  

```
from string import ascii_lowercase as letters
checkio = lambda text: max(letters, key=text.lower().count)
```

The checkio webpage providing the solutions is only available to users who have solved the challenge, so I can't simply give you the url. I decided veky's explanation is worth posting here.

When asked to explain his solution and the difference between bound and unbound methods,  **veky** had this to say (in response to a question):

> Np. Glad you learned something. BTW the concept of bound methods is much more important lesson here than lambda. ;-) [Especially since it can be used to avoid an unnecessary lambda.;]

> First, when trying to grasp language concepts, please refer to Py3 documentation, not Py2. The documentation is clearer, but more importantly, the _language_ itself is clearer and has fewer basic concepts. It’s always better to learn something new on Py3, and then only if you’re curious or you need to, see what are the differences on Py2.

> Case in point: Py3 has only one kind of classes, and bound methods work the same for all of them. Py2 has two kinds, “classic” and “modern” classes, which are irreducible one to another, and have slightly different notions of bound methods. Also, Py2 has the notion of unbound method as a separate object - in Py3, “unbound method” is just an ordinary function. And so on.

> Since you want me to use (natural) language rather than code, I’ll use circumlocution to answer your question. :-P In my code, neither the `lambda` (called `checkio`) nor `max` are bound methods. Bound methods are what you get when you access the attribute on an instance, which on the class is an ordinary function. So, if `A.f` is a function, and `isinstance(a, A)`, (usually) `a.f` is a bound method.

> What’s the difference between `A.f` and `a.f`? They are both callable, but they (usually) differ in the number of arguments they are callable with. If `A.f` is a function accepting three arguments (`self`, `x` and `y`), then `a.f` is callable with two arguments, named `x` and `y`. In the body of `f`, the name `self` refers to `a` itself. So, we can say  
```
a.f(3, 5)    <~~~>    A.f(a, 3, 5)
```
This has many benefits, but the one I use here is cheap specialization. That `f` above probably does something with `self`, with `x` and with `y`, but there are many cases when what it does with `self` is _common_ to many invocations. In other words, it’s called many times with the same `self`, while `x` and `y` vary.

> In this concrete example, the `key` parameter to `max` is a function. It counts how many times a letter appears in text (lowered, but let’s ignore that for now). We can write

```
str.count(text, 'a'), str.count(text, 'b'), str.count(text, 'c'), ...

```
but in fact all of these use the same first argument, while second argument is the one that key function is expecting. We can write   
```
, key=lambda x: str.count(text, letter)
```
but in fact bound methods give us a much easier way. Since `str.count(text, letter)` is the same as `text.count(letter)`, we have a perfectly fine callable thing to set `key` to. Simply

> key=text.count

> Clearer?
