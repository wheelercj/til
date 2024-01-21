+++
title = 'Creating custom terminal commands'
date = 2022-03-20T18:12:52-08:00
lastmod = 2023-08-26T07:17:21-08:00
+++

Creating custom terminal commands can change having to type something long like this:

`py -3.10 "C:\Users\chris\Documents\programming\refactor-todo-list\create_task.py"`

to something like this:

`todo`

This will work no matter which directory the terminal is in and can temporarily change directories and/or activate a virtual environment if needed.

Some programming languages have their own tools for creating custom terminal commands (links to a few are listed below), but sometimes creating the command in one of the other ways on this page is easier overall.

* [Go](https://go.dev/doc/tutorial/compile-install) – compile and install the application
* [Python](https://stackoverflow.com/questions/48884796/how-to-set-up-entry-points-in-setup-cfg) – how to set up entry_points in setup.cfg

## Mac and Linux

[This guide](https://medium.com/devnetwork/how-to-create-your-own-custom-terminal-commands-c5008782a78e) seems well-written (no need to rewrite the wheel).

## Windows

I recommend checking out [Windows Terminal](https://aka.ms/terminal) if you're choosing a terminal app.

### temporary commands

If you already have an executable file, a super quick way to create a command that only lasts until you close the terminal is to run `$env:Path += ';C:\path\to\my\executable\file.exe'` in PowerShell.

### permanent commands

1. In PowerShell, enter `notepad $profile`. This should open a PowerShell file (the file extension should be `.ps1`).
2. In this file, you can create custom terminal commands by defining PowerShell functions. For example,

```powershell
function hi {
    Write-Host "hello"
}
```

This creates a `hi` command that responds with `hello` when used.

3. Save the file.
4. Restart your terminal.
5. Try your new command.

Here are more examples:

```powershell
# This function runs a program.
function matrix {
    & "C:\Users\chris\Documents\programming\the_matrix\x64\Debug\the_matrix.exe"
}

# You can run any type of executable file this way, not just .exe files.
function psql {
    & "C:/ProgramData/Microsoft/Windows/Start Menu/Programs/PostgreSQL 15/SQL Shell (psql).lnk"
}

# This runs a Python program. The $args at the end sends any inputs for the command from
# the terminal to the program. If all the inputs should be in one string, you can put
# double quotes around it: "$args". Note that any inputs with commas on the command-line
# will still need quotes around them for all the input to be in one string.
function rand {
    py C:/Users/chris/Documents/programming/rand/main.py $args
}

# Some programs need to temporarily change the directory and/or activate a virtual
# environment while running.
function todo {
    $originalPath = pwd
    cd C:/Users/chris/Documents/programming/refactor-todo-list
    try {
        venv/Scripts/Activate.ps1
        try {
            py create_task.py "$args"
        } finally {
            deactivate
        }
    } finally {
        cd $originalPath
    }
}

# Make a folder easier to open.
function binds {
    explorer "C:\Users\chris\Documents\programming\binds"
}

# Here's how you can customize what your terminal prompts look like.
function prompt {
    # https://hodgkins.io/ultimate-powershell-prompt-and-git-setup
    $realLASTEXITCODE = $LASTEXITCODE
    Write-Host $($(Get-Location) -replace "\\", "/") -ForegroundColor Blue
    $global:LASTEXITCODE = $realLASTEXITCODE
    return "> "
}

# This command shows or searches your command history across sessions (unlike the built-in
# `h` and `r` commands). This was written by Adam Wemlinger.
function hist {
    # https://superuser.com/questions/1195895/view-full-history-for-powershell-not-just-current-session
    $find = $args; 
    Write-Host "Finding in full history using {`$_ -like `"*$find*`"}"; 
    Get-Content (Get-PSReadlineOption).HistorySavePath | ? {$_ -like "*$find*"} | Get-Unique | more 
}

# Activate a Python virtual environment named "venv" by simply entering "venv". For
# environments with something after venv like "venv311", enter "venv 311".
function venv {
    if ($args) {
        Invoke-Expression "venv$args/Scripts/Activate.ps1"
    } else {
        venv/Scripts/Activate.ps1
    }
}
```

If you don't want to add all your commands to one file, you can create a folder, add it to PATH (see [[20220429185353]] how to edit PATH in Windows), and add executable files to that folder. The files can truly be any type of executable file, such as `.exe`, or `.py` if you're using Python, or `.bat` or `.cmd` if you want to use [Batch scripts](https://www.tutorialspoint.com/batch_script/batch_script_quick_guide.htm), or `.ps1` if you would prefer to use [PowerShell commands](https://devblogs.microsoft.com/scripting/table-of-basic-powershell-commands/). After adding these file(s) to the folder, restart your terminal and enter the file's name without the extension to run the command.

## more about PowerShell

* [customizing terminal prompts in Windows](/customizing-terminal-prompts-in-windows)
* [Microsoft's docs](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.3)
* [PowerShell Gotchas](https://stackoverflow.com/questions/803521/powershell-pitfalls/69644807#69644807)
* the `alias` command lists all aliases
* although many PowerShell guides show commands with uppercase letters, like `Get-Location`, PowerShell is not case-sensitive, so you can use `get-location` (or its alias `pwd`)

## how to receive command line arguments

Every widely-used general-purpose programming language has a way to receive command line inputs. Here are guides for a few:

* [C++ command line arguments](/cpp-command-line-arguments)
* [Python's `argparse` library](https://docs.python.org/3/library/argparse.html)
* [Go's `flag` library](https://pkg.go.dev/flag) and the [spf13/cobra](https://github.com/spf13/cobra) framework that builds on top of it
* [Command Line Interface Guidelines](https://clig.dev/) by Prasad et al. includes a list of command-line argument parsing libraries
