+++
title = 'Editing PATH in Windows'
date = 2022-04-29T18:53:53-08:00
+++

Environment variables such as PATH help organize computers to make important apps and files easier to access. You can edit PATH using a GUI or with PowerShell.

## temporary change with PowerShell

* `$env:Path` gets the current contents of the PATH variable.
* `$env:Path += ';C:\my\file\path'` appends a file or folder to PATH.
* `$env:Path = 'C:\my\file\path;' + $env:Path` prepends a file or folder to PATH.

Changes to PATH made this way will only last until you close the terminal.

## permanent change with a GUI

1. Press the Windows key.
2. Type `path` and select "edit the system environment variables".
3. In the window that pops up, go to the Advanced tab.
4. Click `Environment Variables`.
5. In the user variables (the top box; see below), select the row that has "Path" in the left column.

![windows-env-var-editor.jpg](/windows-env-var-editor.jpg)

6. Click `Edit`.
7. Click `New`.
8. Click `Browse`.
9. Select the file or folder you want to add to PATH.
10. Click `OK` on each of the new windows.
11. Restart any running terminal for the change to take effect.
