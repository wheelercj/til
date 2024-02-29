+++
title = 'Challenges with SSH agent forwarding in Windows'
date = 2024-02-03T23:33:00-08:00
+++

TLDR: SSH agent forwarding is easier with WSL.

I have a need to occasionally pull Git commits from a private GitHub repo into a production server without using an access token, so I had to [set up a GitHub SSH authentication key pair](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). I didn't want to put the private key on the production server because if the server ever became compromised, my GitHub account would too. (I put passphrases on my SSH keys, but I don't want to depend on that too much.) That's why I needed to also set up [SSH agent forwarding](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

## challenges

I tried following the guides linked above using PowerShell in Windows Terminal, and later also in Git Bash. Everything was fine at first, until I ran `ssh -T git@github.com` to test the SSH connection. It would usually give me the error message `git@github.com: Permission denied (publickey)`, and it would sometimes work correctly for the wrong reasons, such as using the default location and name for the key files or specifying the key path like `ssh -T git@github.com -i path/to/key`. Since I couldn't get it working any other way, it appeared ssh-agent was not handling the key correctly despite `ssh-add -l -E sha256` giving the correct output. My output for `ssh -vT git@github.com` is always the same as the sample incorrect output on [Troubleshooting SSH/Error: Permission denied (publickey)](https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey). Sure enough, when I SSHed into the production server and used `ssh -T git@github.com`, I still would get `git@github.com: Permission denied (publickey)` even when I wasn't getting that error message locally. The troubleshooting page didn't have any other tips that might have helped (I carefully tried everything there many times).

## solution

I tried setting up in WSL and it worked immediately. Maybe I could have gotten it to work in PowerShell or Git Bash eventually, but it didn't seem worth the effort. I considered giving feedback about this so the docs might improve, but the error messages I got didn't actually explain what was wrong beyond that the key could not be found.

Sometimes I need to go through this part of the ssh-agent setup process again for some reason:

```text
eval `ssh-agent -s`
ssh-add ~/.ssh/id_ed25519
```

## SSH agent forwarding risk

[GitHub's page on SSH agent fowarding](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding) has an important warning:

> Warning: You may be tempted to use a wildcard like Host * to just apply [the `ForwardAgent yes` setting] to all SSH connections. That's not really a good idea, as you'd be sharing your local SSH keys with every server you SSH into. They won't have direct access to the keys, but they will be able to use them as you while the connection is established. You should only add servers you trust and that you intend to use with agent forwarding.

I want to point out the second part of that; it's easy to miss.

It appears to essentially say that when you set up SSH agent forwarding to a server, while you are connected to that server, anyone in that server can use any ANY and ALL of your SSH keys (that are in ssh-agent) as if they are you. There is still risk to your GitHub account with this method, but at least it's less risk than putting the private key on the remote server.

This gives me the impression that fine-grained access tokens are not only generally more convenient but also more secure than SSH authentication keys.
