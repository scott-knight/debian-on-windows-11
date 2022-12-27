[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-windows-terminal.md) | [Next Step](configure-windows-terminal.md)

<br/>

# Install oh-my-posh and Required Libraries

This document contains information on how to install oh-my-posh and various libraies used for powershell and zsh themes which use Powerline Icons in the console.

[Oh-my-posh](https://ohmyposh.dev/) is similar to [oh-my-zsh](https://ohmyz.sh/). It works in Windows PowerShell which is used in the Windows Terminal. There's minimal setup needed for running (my personal preference) zsh instances. YOU DO NOT HAVE TO DO THIS STEP if you don't plan on using a powershell or zsh theme which requires Powerline icons.

Sources: [Powerline Setup](https://docs.microsoft.com/en-us/windows/terminal/tutorials/powerline-setup), [Custom Prompt Setup](https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup), [Cascadia Code](https://github.com/microsoft/cascadia-code)

<br/>

## Install and Update Windows PowerShell

These are the steps to install the `Windows PowerShell`. Documentation can be [found here](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows).

1. [Download the MSI installer](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-window) for Windows PowerShell.
2. Once down loaded, install Windows PowerShell
3. It will prompt you to select (with a checkbox) to update using Windows Update. Make sure you select this option.
4. Once installed, it will be selectable in the Windows Terminal as an option.

<br/>

## Install Git For Windows

You need `Git for Windows` for `Posh-Git`.

Download and install [Git for Windows](https://git-scm.com/downloads)

<br/>

## Install Posh-Git

Installation page is [found here](https://github.com/dahlbyk/posh-git#installation)

Basically, while in the PowerShell as an Administrator, run the following:

```sh
Install-Module posh-git -Scope CurrentUser -Force
```

To update `posh-git`, run the following:

```sh
Update-Module posh-git
```

<br/>

## Install Oh-my-Posh (and PowerLine Icons)

The [Powerline Setup doc](https://docs.microsoft.com/en-us/windows/terminal/tutorials/powerline-setup) has detailed instructions for installing `Oh-my-Posh` and the related icons. Follow the notes outlined.

A lot has changed since the early Windows 10 days of installing `Oh-my-Posh`. It's much easier to do now. The [Powerline Setup doc](https://docs.microsoft.com/en-us/windows/terminal/tutorials/powerline-setup) basically describes doing the following:

1. [Install Oh-my-Posh](https://ohmyposh.dev/docs/installation/windows)
2. [Install a Nerd Font](https://ohmyposh.dev/docs/installation/fonts).
3. [Select a Theme](https://ohmyposh.dev/docs/themes)

<br/>

## Notes for oh-my-posh

You can actually use `oh-my-posh` with Linux. However, I prefer `oh-my-zsh`. You can read more about using `oh-my-posh` [here](https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup#set-up-powerline-in-wsl-ubuntu)

<br/>

Now you're ready to [Configure Windows Terminal](configure-windows-terminal.md).

<br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-windows-terminal.md)
