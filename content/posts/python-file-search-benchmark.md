+++
title = 'Python file search benchmark'
date = 2025-05-10T14:35:27-07:00
+++

Out of curiosity, I did a quick benchmark of a few variations of Python code that searches 10,000 file names for the lexicographically last one matching a specific pattern. I measured the average time of 100 trials for each variation.

Here's the result:

```text
without max:
        0.0013002311 seconds
with max:
        0.0001507549 seconds
with max and license:
        0.0014262455 seconds
```

In this case, Python is fast enough that it doesn't matter which approach is used. It's best to avoid premature optimization.

Below is the code that gave the results above. Part of why code like this is sometimes necessary is that functions like [`os.listdir`](https://docs.python.org/3/library/os.html#os.listdir) return entries in an arbitrary order.

```python3
import random
import re
import time


pattern: re.Pattern = re.compile(r"^(\d\d\d)_\w+\.sql$")

file_names: list[str] = []
for i in range(10000):
    rand_s: str = ""
    for _ in range(20):
        rand_s += chr(random.randint(ord("a"), ord("z")))
    file_names.append(str(i).zfill(3) + "_" + rand_s + ".sql")


def main():
    n: int = 100

    total1: float = 0
    for _ in range(n):
        start1: float = time.perf_counter()
        _ = without_max()
        end1: float = time.perf_counter()
        total1 += end1 - start1

    print(f"without max:\n\t{total1 / n:.10f} seconds")

    total2: float = 0
    for _ in range(n):
        start2: float = time.perf_counter()
        _ = with_max()
        end2: float = time.perf_counter()
        total2 += end2 - start2

    print(f"with max:\n\t{total2 / n:.10f} seconds")

    file_names.append("LICENSE")
    total3: float = 0
    for _ in range(n):
        start3: float = time.perf_counter()
        _ = with_max()
        end3: float = time.perf_counter()
        total3 += end3 - start3

    print(f"with max and license:\n\t{total3 / n:.10f} seconds")


def without_max() -> int | None:
    latest: int = -1
    for entry in file_names:
        match: re.Match | None = pattern.match(entry)
        if match:
            v: int = int(match.group(1))
            if v > latest:
                latest = v

    if latest == -1:
        return None
    return latest


def with_max() -> int | None:
    entry: str = max(file_names)
    match: re.Match | None = pattern.match(entry)
    if match:
        return int(match.group(1))
    print(end="")

    latest: int = -1
    for entry in file_names:
        match: re.Match | None = pattern.match(entry)
        if match:
            v: int = int(match.group(1))
            if v > latest:
                latest = v

    if latest == -1:
        return None
    return latest


main()
```
