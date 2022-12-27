[Home](https://github.com/scott-knight/linux-on-windows-11) | [Install Debian](install-debian.md)


# Remove and Uninstall Linux Distros

Unregistering the distro will not uninstall it from your system. It simply deletes the created instance from your file system. When you're ready to unregister a linux distro (or want a fresh setup), be sure to save any files you need from that distro before removing it. Uninstalling it is done with an added step (found below).

<br/>

## Remove the Distro from WSL

Open Powershell and run the following:

```sh
wsl.exe --shutdown
wsl --unregister [distro]-[version]
```

<br/>

EX: With distro name and version (Ubuntu)

```sh
wsl.exe --shutdown
wsl --unregister Ubuntu-22.04
```

OR

```sh
wsl.exe --shutdown
wsl --unregister Ubuntu-Preview
```

<br/>

EX: With distro name only (Debian)

```sh
wsl.exe --shutdown
wsl --unregister Debian
```

<br/>

## Uninstall the Distro from Windows

Once it's unregistered, you can uninstall it. To uninstall it, click the `Start Menu` button, then right-ckick `Ubuntu` and select `Uninstall`

![Screenshot 2022-12-26 083931](https://user-images.githubusercontent.com/516548/209559792-ab468e4f-2c00-49ff-85c1-fb32e7f1a78d.png)

<br/><br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Install Debian](install-debian.md)
