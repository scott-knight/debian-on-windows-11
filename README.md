# Installing Debian on Windows 11

This content demonstrates how to setup Debian on Windows 11, to semi-replicate a Mac terminal setup for developing Ruby on Rails (or any other code you would want to use).

<br/>

### DISCLAMER

I use this documentation for my own purposes, but you, the reader, are allowed to use this information for your own purposes as well. These instructions are given only for demonstration purposes, they are not a definitive guide. Follow (use) these instructions at your own risk. You bear the full responsibility of the outcome for following (using) them. By using these instructions, you agree to own and accept the full liablity of the outcome or result. Additionally, you are welcome to fork this project/information and/or submit pull requests (PRs), to add to the information. I retain the right to accept or reject any PR for any reason. You are welcome to write up your own doc and post it where you want if you don't agree with what's posted.

<br/>

### INFO
Below is the step-by-step guide describing how to install all the bits needed to get a Linux (Debian) instance installed, set up, and customized to a state where you can use a console session to write and push code. I created this guide as a safety measure for restoring a destroyed Windows 11 installation and/or my Debian installation (which has happened several times). That being said, this is the list of things that need to be done in order to get things working:

1. [Install WSL2](install-wsl2.md)
2. [Install VSCode (if you want)](install-vscode.md)
3. [Install Windows Terminal](install-windows-terminal.md)
4. [Install oh-my-posh and required libraries](install-oh-my-posh-and-required-libraries.md)
5. [Configure Windows Terminal](configure-windows-terminal.md)
6. [Install Debian](install-debian.md)
7. [Customize Debian](customize-debian.md)
8. [Unregister (from WSL) and Uninstall](unregister-and-uninstall.md)

### IMPORTANT NOTES

Steps 1-5 are Windows setup instructions. Once you have completed steps 1-5, you shouldn't have to do them again. You will be able to create and destroy Linux installs without having to repeat steps 1-5.

Once Windows Terminal is setup, you should be good for the lifetime of your Windows install (pending needed updates if there are any).

You will need to repeat steps 6-7 if you decide to delete your current install of Linux and reinstall it.
