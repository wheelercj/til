+++
title = "Python's islice and unpacking"
date = 2022-11-04T18:26:34-08:00
+++

```python
a = [1, 2, 3, 4]
print(a[1:3])  # [2, 3]

# Slicing makes it easy to get part of a list, but can be
# inefficient because it creates a new list and copies values.

print(*a)  # 1 2 3 4
# This is called unpacking.
print(*a)  # 1 2 3 4
# We can unpack a list as many times as we want.

# To avoid copying when slicing, we can use islice:

from itertools import islice

b = islice(a, 0, 4)
print(*b)  # 1 2 3 4
print(*b)  # (the only output is an empty line)

# There's no output the second time because islice doesn't make
# a new list; it just uses an iterator over the existing list.
# The first unpacking moved the islice object's iterator to
# the end of the list.

print(*a)  # 1 2 3 4
# The list itself is unaffected.

c = islice(a, 0, 4)
a[0] = 0
a[1] = 0
a[2] = 0
a[3] = 0
print(*c)  # 0 0 0 0
```
