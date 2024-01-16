+++
title = 'C++ command-line arguments'
date = 2023-06-15T21:00:50-08:00
+++

![custom-terminal-command-demo.png](/custom-terminal-command-demo.png)

Sometimes it's helpful to create your own terminal commands. This can be done as explained in [creating custom terminal commands](/creating-custom-terminal-commands), but if your custom command runs another program, receiving inputs (like the two numbers above) from the custom command to your program is another matter.

Every widely-used general-purpose programming language has a way to get command line arguments. Most languages have libraries to help with the parsing, such as Python's [argparse](https://docs.python.org/3/library/argparse.html) library or Go's [flag](https://pkg.go.dev/flag) and [Cobra](https://github.com/spf13/cobra) libraries. There are third-party libraries for this for C++, but if you don't want to use one of those, you can do the parsing yourself as shown below.

```cpp
#include <iostream>
using namespace std;

int main(int argc, char* argv[])
{
    int sum = 0;
    for (int i = 1; i < argc; i++)
    {
        sum += atoi(argv[i]);
        if (i < argc - 1)
            cout << argv[i] << " + ";
    }
    cout << argv[argc - 1] << " = " << sum << endl;
    return 0;
}
```

The unusual part is that the main function is taking inputs, `int argc, char* argv[]`. The parameter names `argc` and `argv` can be almost anything you want, but their types and order are important. `argv` (or whichever name you choose) is an array of c-strings of all the inputs to the program (the **arg**ument **v**alues). `argc` is the size of the `argv` array (the **arg**ument **c**ount). The first element of `argv` is always the path to the program.

After setting up a custom terminal command for this (example below), using the terminal command `add 267 917` puts the value `"267"` in `argv[1]` and `"917"` in `argv[2]`. As shown above, these c-strings of numbers can then be converted to ints with the `atoi` function and added together.

For the custom terminal command, I followed the steps in [creating custom terminal commands](/creating-custom-terminal-commands) and created this PowerShell function:

```powershell
function add {
    & "C:\Users\chris\source\repos\Project1\x64\Debug\Project1.exe" $args
}
```

## see also

* [`main` function and command-line arguments](https://learn.microsoft.com/en-us/cpp/cpp/main-function-command-line-args?view=msvc-170)
* [customizing terminal prompts in Windows](/customizing-terminal-prompts-in-windows)
