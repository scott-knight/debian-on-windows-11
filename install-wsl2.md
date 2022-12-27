[Home](https://github.com/scott-knight/linux-on-windows-11) | [Next Step](install-vscode.md)

<br/>

# Install Windows 11 WSL 2

This document explains how to install Windows 11 WSL 2.

## Installation Steps

1. Enter your computers BIOS and make sure (Hyper-V) virtualization is enabled (if it isn't already). Save the settings and reboot.
2. After rebooting, click the Windows Icon and the Settings icon
3. Once settings is open, click Apps, then Optional Features, then scroll to see the More Windows Features selection. Click, More Windows features:

![apps-optional-features](https://user-images.githubusercontent.com/516548/191402388-f7504f4a-1ae3-49f1-8efc-2c653b2787bd.png)

4. Select, Virtual Machine Platform and Windows Subsystem for Linux.

![windows selection](https://user-images.githubusercontent.com/516548/191402641-3bd76611-842b-4f7c-836e-d163b8527f0c.png)

5. Reboot (if prompted)
6. After the reboot, open PowerShell as Administrator (repeat step 2)
7. Run the following commands in the console::

```sh
wsl --set-default-version 2
```

WSL2 will be installed and ready to go. Now you can move on to the next step, [install VSCode](install-vscode.md).

<br/>

[Home](https://github.com/scott-knight/linux-on-windows-11)
