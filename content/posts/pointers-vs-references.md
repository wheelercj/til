+++
title = 'Pointers vs. references'
date = 2024-07-03T14:17:41-07:00
+++

Some differences between pointers and references can be confusing, especially since different programming languages define references in different ways.

Pointers can point anywhere in memory. They can point to null, or to memory with data of the pointer's type, or anywhere else. Besides various pointer safety features some languages have, there are no restrictions on where pointers can point.

References can refer to memory with data of the reference's type. References in some languages, like C++, allow this and nothing else. However, most languages also allow references to refer to null. In any case, references cannot refer to memory with data that is not of the reference's type.

To make things more complicated, some definitions of "references" disagree on whether references need to be able to be "returned by reference" (see description below) even when reassigned. This is especially confusing in Go. One of the language's project members, Dave Cheney, explains that [There is no pass-by-reference in Go](https://dave.cheney.net/2017/04/29/there-is-no-pass-by-reference-in-go), yet the official Go FAQ says [maps, slices, and channels are references](https://go.dev/doc/faq#references). (I ran Cheney's sample code with Go 1.22.5 and it gave the same output.) Whether Go has references depends on the debatable definition of "references", but in my experience, most people say Go has references.

Related: [Value, reference, and move types and semantics](/value-reference-and-move-types-and-semantics)

## Returned by reference

Here's what "returned by reference" means:

1. a function calls another, giving it a reference variable
2. the called function changes the variable but does not return it
3. the called function ends
4. the calling function resumes, but the variable still has the changes made by the called function as if it was returned

Both functions accessed the same copy of the reference variable, the same part of the computer's memory.

All of this is true in Go when only *mutating* a map, slice, or channel, but not when *reassigning* it. Returning nothing after reassigning a map, slice, or channel does nothing to the variable. My guess is that this behavior makes Go's garbage collection more efficient since the scope of dynamically allocated memory is more predictable. Fortunately, the static analysis tools most people install by default seem to catch all coding mistakes related to this.
