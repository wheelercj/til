+++
title = 'Customizing Git'
date = 2024-03-21T12:35:53-07:00
+++

There are many ways you can customize Git. One of the most useful ways is by creating command aliases. For example, you could create `git ds` so you don't have to type `git diff --staged`. To create this alias, open (or create) a file named `~/.gitconfig` and add this:

```text
[alias]
	ds = diff --staged
```

If you already have an `[alias]` section, add `ds = diff --staged` in that section.

Aliases are for more than just making existing commands easier to use. Git and its alias system are powerful enough that you can essentially create entirely new commands, such as [Slipp D. Thompson's log commands](https://stackoverflow.com/questions/1838873/visualizing-branch-topology-in-git/34467298#34467298).

Git also allows you to create new commands (or even replace existing ones) with an executable file. For example, you can create a `git dft` command that uses [Difftastic](https://github.com/Wilfred/difftastic)'s executable.

## see also

* [So You Think You Know Git - FOSDEM 2024 - YouTube](https://www.youtube.com/watch?v=aolI_Rz0ZqY) covers many other .gitconfig options and Git commands.
* [Getting started with Git and GitHub](https://chriswheeler.dev/posts/getting-started-with-git-and-github/)
* [Creating custom terminal commands](https://til.chriswheeler.dev/creating-custom-terminal-commands/)
* [Creating a GPG key for signing Git commits](https://til.chriswheeler.dev/creating-a-gpg-key-for-signing-git-commits/)
