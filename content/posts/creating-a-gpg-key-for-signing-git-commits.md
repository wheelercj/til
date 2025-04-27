+++
title = 'Creating a GPG key for signing Git commits'
date = 2024-01-25T13:10:00-08:00
lastmod = 2024-11-03T22:21:40-08:00
+++

I'm reading [What is Commit Signing in Git?](https://www.freecodecamp.org/news/what-is-commit-signing-in-git) by freeCodeCamp. It suggests using Git Bash.

## custom Windows Terminal profile

I don't like using Git Bash directly, so I made a custom Windows Terminal profile for Git Bash by following the instructions in [Using Git Bash with the Microsoft Terminal](https://scribe.rip/@techpreacher/using-git-bash-with-the-microsoft-terminal-bd1f71fa17a1) by Sascha Corti. I removed some unnecessary lines and made the `guid` string one line so that it was valid JSON. Also, Git Bash was opening to system 32 by default for some reason, so I found in [the official Windows Terminal docs](https://learn.microsoft.com/en-us/windows/terminal/customize-settings/profile-general) the `startingDirectory` property and what its value should be. Here's what I ended up with:

```json
{
      "guid": "{00000000-0000-0000-0000-000000012345}",
      "hidden": false,
      "name": "Git Bash",
      "commandline": "\"%PROGRAMFILES%\\git\\bin\\bash.exe\" --login -i -l",
      "icon": "%PROGRAMFILES%\\git\\mingw64\\share\\git\\git-for-windows.ico",
      "startingDirectory": "%USERPROFILE%"
}
```

## guides and tools for GPG keys

Later, I found other potentially helpful guides: [Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits) by GitHub, and [7.4 Git Tools - Signing Your Work](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work) on Git's official site. [How (and why) to sign Git commits](https://withblue.ink/2020/05/17/how-and-why-to-sign-git-commits.html), by Alessandro Segala, gives some examples of why to sign Git commits.

It sounds like [Gpg4win](https://www.gpg4win.org/) is the easiest way to sign commits in Windows, but I finished the [gpg-agent](http://linux.die.net/man/1/gpg-agent) setup before finding that out.

GPG keys can be reused, but not all GPG keys are compatible with Git and GitHub.

## gpg commands

These can run in Git Bash and some other shells, but not PowerShell.

* `gpg --version` to make sure gpg is installed.
* `gpg --list-keys` to list GPG keys.
* `gpg --full-gen-key` to generate keys, such as an RSA key pair. When it asks for your email address, it's important to use the address that you commit with.
* `gpg --export --armor putAKeyFingerprintHere > ./gpg-key.pub` to export the public key to a file named `gpg-key.pub`. The `--armor` option makes the file contents ASCII rather than binary. It's fine to share the public key with multiple services (GitHub, GitLab, etc.).
* `gpg --export-secret-keys --armor putAKeyFingerprintHere > ./gpg-key.asc` to export the private key so that it can be backed up and used from multiple devices.
* `git config --global commit.gpgsign true` to enable signing commits with the GPG key.
* `git config --global user.signingkey putAKeyFingerprintHere` to specify which key should be used to sign commits.

Don't forget to delete exported key files after using them.

## sample outputs

Here's the output from generating a key in Git Bash (with `gpg --full-gen-key`), after answering the prompts:

```shell
gpg: directory '/c/Users/chris/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/c/Users/chris/.gnupg/openpgp-revocs.d/keyFingerPrintShownHere.rev'
public and secret key created and signed.

pub   rsa4096 2024-01-25 [SC]
      keyFingerPrintShownHere
uid                      Chris Wheeler <chrisw289@gmail.com>
sub   rsa4096 2024-01-25 [E]
```

Here's the output from `gpg --list-keys`:

```shell
$ gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
/c/Users/chris/.gnupg/pubring.kbx
---------------------------------
pub   rsa4096 2024-01-25 [SC]
      keyFingerPrintShownHere
uid           [ultimate] Chris Wheeler <chrisw289@gmail.com>
sub   rsa4096 2024-01-25 [E]
```

A key's fingerprint is kind of like its name.

I saved my public and private keys to my password manager, but I'm not sure how to set up a new device with existing keys. I'll figure that out when I need to.

## caching the password

The key's password is being requested on almost every commit, which is annoying. [This Stack Exchange](https://superuser.com/questions/624343/keep-gnupg-credentials-cached-for-entire-user-session) discussion describes how to increase how long the password is cached by gpg-agent. If the file `gpg-agent.conf` doesn't exist, it's fine to create it.

Device restarts clear the cache.

## moving to Ubuntu

I'm switching from Windows 11 to Ubuntu. I copied my `.gitconfig` file without changes. It has my name, email, & signing key, and `gpgsign` is set to true. When I first tried to commit in Ubuntu, I got the error message "error: gpg failed to sign the data". To fix this, I needed to copy/download my secret key I saved from Windows 11, run `gpg --import secret-key.asc` on it, and then delete the secret key file. I don't know if all secret keys have the .asc extension. I was then able to confirm the import with `gpg --list-keys`. Now I am able to commit in Ubuntu.
