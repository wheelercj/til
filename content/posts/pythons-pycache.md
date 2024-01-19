+++
title = "Python's pycache"
date = 2021-05-16T10:10:07-08:00
lastmod = 2021-09-23T18:36:33-08:00
+++

When working on a python project, always add `__pycache__` to the gitignore! Better yet, start projects with a [.gitignore template](https://github.com/github/gitignore) for whichever language and tools you're using.

## when gitignore isn't ignoring

If you have already committed `__pycache__` and/or `.pyc` files, use `git rm -r --cached .`. This will remove all files from git's index (what's listed when you use `git status`). Then you add back the files you want to keep in the index.

A different option that _might_ work is using `git update-index --skip-worktree <file_name>` to remove the `.pyc` files from the index. "This is to tell git you want your own independent version of the file or folder. For instance, you don't want to overwrite (or delete) production/staging config files. . . . It's important to know that `git update-index` **will not propagate** with git, and each user will have to run it independently" ([source](https://stackoverflow.com/questions/936249/how-to-stop-tracking-and-ignore-changes-to-a-file-in-git)). Samples of how to use this command:

* `git update-index --skip-worktree __pycache__/detect.cpython-39.pyc`
* `git update-index --skip-worktree __pycache__/track.cpython-39.pyc`
* `git update-index --skip-worktree __pycache__/process.cpython-39.pyc`

## what is pycache?

"As a programmer, you can largely just ignore it... All it does is make your program start a little faster. When your scripts change, they will be recompiled. . . . When you're sending your code to other people, the common practice is to delete that folder, but it doesn't really matter whether you do or don't. When you're using version control (`git`), this folder is typically listed in the ignore file (`.gitignore`) and thus not included" ([source](https://stackoverflow.com/questions/16869024/what-is-pycache)).

## what is a .pyc file?

A `.pyc` (Python Compiled) file is an "executable file that contains compiled source code written in the Python programming language. . . . PYC files primarily contain Python bytecode. A bytecode is an instruction set executed by its designated software interpreter. Bytecode is the result of compiling source code written in a specific programming language. The virtual machine converts each bytecode into a specific machine instruction that the computer processor understands. Since Python instruction sets are bytecodes, they have to be converted before it can be interpreted and finally executed" ([source](https://file.org/extension/pyc)).
