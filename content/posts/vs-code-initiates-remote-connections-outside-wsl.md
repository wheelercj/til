+++
title = 'VS Code initiates remote connections outside WSL'
date = 2024-02-14T16:26:15-08:00
+++

Or at least this appears to be the default behavior.

I ran a VPN connection in WSL, opened a remote connection to WSL in VS Code, and then tried to use VS Code's remote explorer to connect to a remote server via SSH. I needed VS Code to initiate SSH from within WSL so that the VPN would be used. However, it always failed. Here's part of the error message:

```log
[21:37:35.129] Checking ssh with "C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common\ssh.exe -V"
[21:37:35.130] Got error from ssh: spawn C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common\ssh.exe ENOENT
[21:37:35.131] Checking ssh with "C:\Program Files\Microsoft\jdk-11.0.16.101-hotspot\bin\ssh.exe -V"
[21:37:35.132] Got error from ssh: spawn C:\Program Files\Microsoft\jdk-11.0.16.101-hotspot\bin\ssh.exe ENOENT
[21:37:35.132] Checking ssh with "C:\WINDOWS\system32\ssh.exe -V"
[21:37:35.133] Got error from ssh: spawn C:\WINDOWS\system32\ssh.exe ENOENT
[21:37:35.133] Checking ssh with "C:\WINDOWS\ssh.exe -V"
[21:37:35.134] Got error from ssh: spawn C:\WINDOWS\ssh.exe ENOENT
[21:37:35.134] Checking ssh with "C:\WINDOWS\System32\Wbem\ssh.exe -V"
[21:37:35.134] Got error from ssh: spawn C:\WINDOWS\System32\Wbem\ssh.exe ENOENT
[21:37:35.135] Checking ssh with "C:\WINDOWS\System32\WindowsPowerShell\v1.0\ssh.exe -V"
[21:37:35.135] Got error from ssh: spawn C:\WINDOWS\System32\WindowsPowerShell\v1.0\ssh.exe ENOENT
[21:37:35.135] Checking ssh with "C:\WINDOWS\System32\OpenSSH\ssh.exe -V"
[21:37:35.165] > OpenSSH_for_Windows_8.6p1, LibreSSL 3.4.3

[21:37:35.171] Using SSH config file "\\wsl.localhost\Ubuntu\home\chris\.ssh\config"
[21:37:35.171] Running script with connection command: "C:\WINDOWS\System32\OpenSSH\ssh.exe" -T -D 12345 -F "\\wsl.localhost\Ubuntu\home\chris\.ssh\config" hostName bash
[21:37:35.173] Terminal shell path: C:\WINDOWS\System32\cmd.exe
[21:37:52.187] Resolver error: Error: Connecting with SSH timed out
	at g.Timeout (c:\Users\chris\.vscode\extensions\ms-vscode-remote.remote-ssh-0.108.0\out\extension.js:2:460371)
	at Timeout._onTimeout (c:\Users\chris\.vscode\extensions\ms-vscode-remote.remote-ssh-0.108.0\out\extension.js:2:579770)
	at listOnTimeout (node:internal/timers:569:17)
	at process.processTimers (node:internal/timers:512:7)
[21:37:52.198] ------
```

The only SSH executables it attempted to use were Windows ones. The connection probably timed out because I needed to connect using the VPN running in WSL, but VS Code's connector tried to connect from outside WSL. The fact I had needed to set the SSH config path to `\\wsl.localhost\Ubuntu\home\chris\.ssh\config` for VS Code to find the right config was already a sign something would go wrong; if I set it to `~/.ssh/config`, it would only load the SSH config I had outside WSL.

I searched and found a VS Code setting, `remote.SSH.path`. I tried different values for it including `/usr/bin/ssh` and `\\\\wsl.localhost\\Ubuntu\\usr\\bin\\ssh`, but they would always give the same error as above with something like this added:

```log
[22:39:36.935] Checking ssh with "/usr/bin/ssh -V"
[22:39:36.936] Got error from ssh: spawn /usr/bin/ssh ENOENT
[22:39:36.936] The specified path /usr/bin/ssh is not a valid SSH binary
```

I think it could only work with a Windows executable file.

## solution

I downloaded the Windows version of OpenVPN Connect, and fortunately all the same files for making the connection in WSL worked outside WSL too. With my SSH config moved into Windows and the VS Code setting for where my SSH config was changed to `~/.ssh/config`, VS Code's remote connector used the VPN and successfully connected!
