+++
title = 'Value, reference, and move types and semantics'
date = 2024-01-23T23:55:59-08:00
lastmod = 2024-02-04T14:17:44-08:00
+++

I see a lot of confusion about value types and references types. Although I'm not sure how common this perspective is, here's how I think of it.

First of all, value types have value semantics and reference types have reference semantics. The semantics of a type is the behavior of variables of that type.

Let's say there are two variables, `a` and `b`, that have already been created and have the same type. If we assign one to the other, what exactly happens?

## value semantics

`a = b` makes a new copy of the data in `b` and saves it in `a`. The result is that `a` and `b` each have their own copy of the data.

## reference semantics

`a = b` makes `a` just another name, an alias, for `b`. From now on, any change to one happens to the other as well because they are two names directly referring to one instance of data.

## move semantics

`a = b` relabels `b`'s data as belonging to `a`, making `b` empty. Some languages have a move function for move semantics: `a = move(b)`.

## assignment happens constantly

The examples above are the most obvious form of assigning one variable to another, but assignment also happens in other situations, such as when a function is called with arguments. The arguments of the function call are assigned to the function's parameters. Semantics plays a role here as well.

## pointers

At least in most programming languages, pointers have value semantics. It might seem like they have reference semantics because assigning one to another results in both pointing to the same instance of data. However, what matters is the data **directly** involved in assignment. Assignment of pointers makes a new copy of a memory address, so pointers have value semantics.

## where do we see these categories of types?

Some languages, such as C, only have value types. Most have value and reference types, and only a small number have all three. Currently, the only languages I know to have move semantics (as well as value and reference semantics) are C++ and Rust.

Note that commonly used terminology for these ideas differs between languages. The phrases "pass by reference", "pass by value", and "return by reference" are used in some communities when referring to how function call arguments are assigned to function parameters. In the Python community, people usually talk about mutability and immutability instead of values and references because, in Python, everything mutable is returned by reference if it hasn't been reassigned.

I never heard the phrases "value types" and "reference types" until I started learning C#, after I learned C, C++, Java, JavaScript, and Python. However, these ideas appear to generally apply to all languages.

## further reading

* [Pointers vs. references](/pointers-vs-references)
* [C++ Move Semantics Considered Harmful (Rust is better)](https://www.thecodedmessage.com/posts/cpp-move/) by Jimmy Hartzell
* [C++'s std::move function](https://en.cppreference.com/w/cpp/utility/move)
