[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](configure-windows-terminal.md) | [Next Step](customize-debian.md) | [WSL Basic Commands](https://learn.microsoft.com/en-us/windows/wsl/basic-commands)


# Install Debian
Debiain is a thinner install of Linux than Ubuntu *(Ubuntu is a wrapper or enhancement of Debain)*, and sets up a bit easier as well.

*I find that Windows and WSL installs change often. If things don't work as described in this doc, they changed something. By the time you read this doc, it's possible that some of these steps may no longer be required. It's also possible that new steps will be required to get everything working. Either way, I do what I can to keep this document updated, but be prepared to troubleshoot issues as they arise.*

<br/>

## Removing Debian

*Important:* Everything in the debian instance will be lost when you uninstall it. If you have content (pictures, files, ssh keys, etc) that you want to save, you will need to save that content before removing the debian instance. If you need to remove an installation of debian, it's simple. In the `Windows PowerShell` (running as administrator), run the following

```bash
wsl.exe --shutdown
wsl.exe --unregister Debian
```

[Complete removal instructions](https://github.com/scott-knight/linux-on-windows-11/blob/main/unregister-and-uninstall.md)

<br/>

## Update WSL

To ensure you have the latest version of WSL, open the Windows PowerShell as an Administrator.

<br/>

![run-as-administrator](https://user-images.githubusercontent.com/516548/192077877-6748108f-fdd2-4c83-b0ba-3ac31224c9bf.png)

<br/>

Once open, run the following:

```sh
wsl --update
```

A complete list of [WSL commands can be found here](https://learn.microsoft.com/en-us/windows/wsl/basic-commands)

<br/><br/>

## Installing Debian

1 . To install Debian, in the `Windows PowerShell` (running as administrator), run the following:

```sh
wsl.exe --install -d Debian
```

<br/>

2. Once downloaded and installed, it will open a new terminal instance. You will be promted to create a username and password. Once entered, the setup will complete.

![debian-setup](https://user-images.githubusercontent.com/516548/192112953-e95b93a0-5c68-407a-8ae3-ea0b15ad8fe4.png)

<br/>

3. When finished, click the down-arrow in the console's tab bar, then click `Settings`.

![new-settings](https://user-images.githubusercontent.com/516548/192082679-8cc094a2-e920-4b00-943e-91a3e75ccb4b.png)

<br/>

4. On the left-nav, scroll down and click `Debian`. On the right, select `Apperance`. Change the color scheme to `Campbell` and the font face to `CaskaydiaCove Nerd Font Mono`. Then click `Save` and close the settings tab.

![debian-font](https://user-images.githubusercontent.com/516548/193384119-47cb6b12-ffdb-468d-b65b-76b004b6b062.png)

<br/><br/>

## Update Debian and Install System Utilities

1. To update Debian, run the following:

```sh
sudo bash -c 'for i in update {,dist-}upgrade auto{remove,clean}; do apt-get $i -y; done'
```

<br/>

2. Install system utilities by running the following:

```sh
sudo apt-get install -y apt-transport-https aptitude autoconf bison build-essential checkinstall clang curl ca-certificates gcc git gpg gnupg2 libssl-dev libpq-dev libyaml-dev libreadline-dev libncurses-dev libffi-dev libgdbm6 libgdbm-dev libdb-dev lsb-release libxml2-dev libxslt-dev make patch pkg-config software-properties-common wget vim zlib1g-dev liblzma-dev zsh
```

<br/>

3. Install VIPS libraries (used by Rails to manage images):

```sh
sudo apt-get install -y libglib2.0-0 libglib2.0-dev libpoppler-glib8 libheif-dev libvips-dev libvips
```

<br/>

4. Once everything is installed, run the following:

```sh
sudo aptitude full-upgrade
```

<br/>

Now you're ready to [Customize Debian](customize-debian.md)

<br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](configure-windows-terminal.md)
