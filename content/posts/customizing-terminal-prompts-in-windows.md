+++
title = 'Customizing terminal prompts in Windows'
date = 2023-02-06T21:39:46-08:00
lastmod = 2023-02-08T18:48:31-08:00
+++

Which looks better?

![powershells-default-look.png](/powershells-default-look.png)

![custom-terminal-prompt-demo.png](/custom-terminal-prompt-demo.png)

The second one, of course. The color is nice, but most importantly, what you type will appear on the next line after the current path. Yet, the first is the default in Windows for many terminals (like the VS Code terminal, Windows Terminal, PowerShell, etc.).

Here's how to make the change for all terminals:

1. In any terminal, enter `notepad $profile`. This should open a file.
2. In that file, paste this:

```powershell
# https://hodgkins.io/ultimate-powershell-prompt-and-git-setup
function prompt {
    $realLASTEXITCODE = $LASTEXITCODE
    Write-Host $($(Get-Location) -replace "\\", "/") -ForegroundColor Blue
    $global:LASTEXITCODE = $realLASTEXITCODE
    return "> "
}
```

3. Save the file and restart the terminal.

Now you should see something like this:

![new-terminal-prompt.png](/new-terminal-prompt.png)

There are also many other prompt customizations possible such as showing only the current folder instead of the full path, or replacing the home directory with `~`. Here's a guide that shows some other customizations (not just for PowerShell): [Ultimate PowerShell Prompt Customization and Git Setup Guide](https://hodgkins.io/ultimate-powershell-prompt-and-git-setup) by Matthew Hodgkins.
