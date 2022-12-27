[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-debian.md) | [Uninstall](unregister-and-uninstall.md)

<br/>

# Customize Debain

This doc outlines the specifics for setting up the Debian environment for Ruby, Rails, Node, etc.

<br/>

## Connecting VSCode

1. In the Linux console, type the following:

```sh
code .
```

This will load VSCode and connect to your Debian instance, and you will see the files of your home directory.

<br/>

2. Close VSCode and the terminal

<br/>

## Environment Setup

Next, we need system files for the environment. Run the following:

```sh
touch .zsh_functions .zsh_alias_list .gemrc .gitconfig && mkdir dev.projects dev.projects/sandbox-js dev.projects/sandbox-api && mkdir .local/bin && touch .local/bin/wslopen
```

<br/>

## Setup `wslopen` for letter_opener

In a rails project, it's possible to use the [letter_opener gem](https://github.com/ryanb/letter_opener) for posting email in the dev environment. The letter_opener gem uses the launchy gem to launch/post generated email to a browser tab. On a Mac (or possibly a native Linux setup) the browser is set by the system and launchy just works. However, with WSL we have to make the browser connection for launchy. In this example, we will point to location on the Windows drive for [Brave Browser](https://brave.com)

Brave is installed on the `C` drive in the following location: `C:\Program Files\BraveSoftware\Brave-Browser\Application\brave.exe`. This needs to be translated to a WSL2 path: `/mnt/c/Program\ Files/BraveSoftware/Brave-Browser/Application/brave.exe`.

We need to create a couple of files to get everything to work:

```zsh
mkdir $HOME/.local/bin
```

<br/>

In the code snippet below, you can replace `/mnt/c/Program\ Files/BraveSoftware/Brave-Browser/Application/brave.exe` with the browser of your choice. Once you have the path to your chosen browser, run the following:

```zsh
echo '#!/usr/bin/zsh' >> $HOME/.local/bin/wslopen && echo '/mnt/c/Program\ Files/BraveSoftware/Brave-Browser/Application/brave.exe "file://$(wslpath -m ${1/"file://"/})"' >> $HOME/.local/bin/wslopen && chmod +x $HOME/.local/bin/wslopen
```

<br/>

Run the following in the console:

```zsh
echo '# .local/bin -- used with letter_opener' >> .zshrc && echo 'export PATH="${HOME}/.local/bin:$PATH"' >> .zshrc && echo 'export BROWSER="wslopen"' >> .zshrc
```

Then reload the shell.

<br/>

## Setup Zsh

Make zsh your default shell, run the following:

```sh
chsh -s $(which zsh)
```

Once changed, restart the Linux instance.

You will be prompted to make a selection to create a `.zshrc` file. Select the option that simply adds the comment code and creates the file.

Close all instances and start a new Linux instance.

<br/>

## Install BREW for Linux

Reference found [here](https://docs.brew.sh/Homebrew-on-Linux)

1. To install BREW for Linux, run the following:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. You should be prompted about default settings and installation. Simply accept the defaults.
3. Once finished, add the following to your `.zshrc` file

```sh
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> $HOME/.zshrc && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

4. Reload the shell.
5. Add BREW taps

```sh
brew tap Homebrew/homebrew-cask && brew tap Homebrew/homebrew-services && brew tap homebrew/cask-versions && brew tap homebrew/cask-fonts
```

6. Install stuff

```sh
ulimit -n 8192 && brew install gcc git python vips
```

Then

```zsh
brew postinstall docbook docbook-xsl
```
<br/>

7. Install Elixir (if you need/want it)

```sh
brew install erlang elixir
```

<br/>

## Install Postgres

Install postgres by doing the following:

```sh
brew install postgresql@15 && echo 'export PATH="/home/linuxbrew/.linuxbrew/opt/postgresql@15/bin:$PATH"' >> $HOME/.zshrc && source $HOME/.zshrc
```

Then copy this in the console:

```zsh
echo '' >> $HOME/.zshrc
echo "# create the postgresql temp file if it doesn't exit" >> $HOME/.zshrc
echo 'function set_pg_dir() {' >> $HOME/.zshrc
echo '  POSTGRESTEMP=/var/run/postgresql' >> $HOME/.zshrc
echo '  if [ ! -d "$POSTGRESTEMP" ]; then' >> $HOME/.zshrc
echo '    echo Creating $POSTGRESTEMP for PostgreSQL' >> $HOME/.zshrc
echo "    echo '1' | sudo -S mkdir $POSTGRESTEMP && echo '1' | sudo -S chmod 0777 /var/run/postgresql" >> $HOME/.zshrc
echo '  else' >> $HOME/.zshrc
echo '    echo $POSTGRESTEMP exists!' >> $HOME/.zshrc
echo '  fi' >> $HOME/.zshrc
echo '}' >> $HOME/.zshrc
echo 'alias setpgdir="set_pg_dir"' >> $HOME/.zshrc
echo 'setpgdir' >> $HOME/.zshrc
echo '' >> $HOME/.zshrc
echo '' >> $HOME/.zshrc
echo 'function pgfix () {' >> $HOME/.zshrc
echo '  PGFILE=/tmp/.s.PGSQL.5432' >> $HOME/.zshrc
echo '  if [ -f "$PGFILE"]; then' >> $HOME/.zshrc
echo "    echo '1' | sudo ln -s $PGFILE /var/run/postgresql/.s.PGSQL.5432" >> $HOME/.zshrc
echo '    echo $PGFILE was linked in /var/run/postgresql/' >> $HOME/.zshrc
echo '  else' >> $HOME/.zshrc
echo '    echo $PGFILE is not available for the fix!' >> $HOME/.zshrc
echo '  fi' >> $HOME/.zshrc
echo '}' >> $HOME/.zshrc
echo '' >> $HOME/.zshrc
source .zshrc
```
<br/>

### Edit postgresql.conf

To get postgres to work on debian, you have to do the following:

<br/>

Find the config file:

```zsh
psql -U [linux username] -d postgres -c 'SHOW config_file'
```
<br/>

EX:

```zsh
psql -U sknight -d postgres -c 'SHOW config_file'
```
<br/>

It will return something like this:

> /home/linuxbrew/.linuxbrew/var/postgresql@15/postgresql.conf

<br/>

Edit the file.

```zsh
nano /home/linuxbrew/.linuxbrew/var/postgresql@15/postgresql.conf
```

<br/>

In the file, find `unix_socket_directories`. Uncomment it and change it to:

```txt
unix_socket_directories = '/var/run/postgresql,/tmp'
```

Then save the file.

<br/>

To create `/var/run/postgresql` (if it doesn't already exist) run the following:

```zsh
setpgdir
```
<br/>

### Start the Postgres server

If you have enabled `systemd`, you can run the following:

```zsh
brew services start postgresql@15
```

OR to simply start it using the postgres command:

```zsh
pg_ctl -D /home/linuxbrew/.linuxbrew/var/postgresql@15 start
```

<br/>

Once it's running it will return something like this:

> waiting for server to start....2022-11-13 20:54:42.075 UTC [26837] LOG:  starting PostgreSQL 15.1 (Homebrew) on x86_64-pc-linux-gnu, compiled by gcc-11 (Ubuntu 11.3.0-1ubuntu1~22.04) 11.3.0, 64-bit
2022-11-13 20:54:42.075 UTC [26837] LOG:  listening on IPv4 address "127.0.0.1", port 5432
2022-11-13 20:54:42.079 UTC [26837] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2022-11-13 20:54:42.085 UTC [26837] LOG:  listening on Unix socket "/tmp/.s.PGSQL.5432"
2022-11-13 20:54:42.090 UTC [26840] LOG:  database system was shut down at 2022-11-13 20:23:23 UTC
2022-11-13 20:54:42.095 UTC [26837] LOG:  database system is ready to accept connections
  done
server started

<br/>

## Setup SSH Key

To connect via ssh to external services you will need to generate a new private and public key. Follow the instructions [found here](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create a new set.

Once your keys are created, run the following:

(Run this if `.ssh` doesn't exist:
```zsh
mkdir -m a=rwx $HOME/.ssh
```

<br/>

### If You Have Existing SSH Files

If you already have ssh files created and stored somewhere, copy and paste them into you .ssh dir

![ssh-files](https://user-images.githubusercontent.com/516548/209577940-c9db2c03-8820-45d0-8c7d-9493adb55405.png)

<br/>

### If You Need to Create SSH Files

```sh
touch $HOME/.ssh/config && nano $HOME/.ssh/config
```

Copy the following to the new `config` file:

```sh
Host *
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519
```

You will need to add the new public key to your github account. You can copy the key by running the following:

```sh
clip.exe < ${HOME}/.ssh/id_ed25519.pub
```

<br/>

If you copy contents from another `.ssh` to this setup, you will may need to change the file level permissions:

```sh
chmod 400 $HOME/.ssh/id_ed25519
```

<br/>

## INSTALL KEYCHAIN

Run the following:

```sh
sudo apt-get install keychain
```

<br/>

Once installed, start `keychain` to create the `$HOME\.keychain` directory and start the `ssh-agent`:

```sh
keychain
```

<br/>

Using VIM or Nano, copy this to the bottom of your .zshrc file:

```zsh
nano .zshrc
```

<br/>

BIGBRAIN is the hostname of my computer. If you run `ls -FlaG $HOME/.keychain` in the console,
you will see the hostname of your computer. Replace BIGBRAIN with that name

```
# Keychain
export HOSTNAME=BIGBRAIN
/usr/bin/keychain --clear $HOME/.ssh/id_ed25519
source $HOME/.keychain/$HOSTNAME-sh
```

<br/>

## Copy gitconfig

Using VIM or Nano, replace the contents of `.gitconfig` with the following:

```zsh
nano .gitconfig
```

<br/>

```sh
[user]
  email = [your email]
  name = [your-username]

[pull]
  rebase = false

[alias]
  co = checkout
  ci = commit
  st = status
  br = branch

[pager]
  branch = false
```

Replace the email and username with your values.

<br/>

## INSTALL RBENV

To install RBENV, run the following:

```sh
git clone https://github.com/rbenv/rbenv.git ${HOME}/.rbenv
```

Add the following to `.zshrc`:

```zsh
nano .zshrc
```

<br/>

```sh
# RBENV
export RBENV_ROOT="${HOME}/.rbenv"
export PATH="${RBENV_ROOT}/bin:${RBENV_ROOT}/shims:$PATH"
if which rbenv > /dev/null; then eval "$(rbenv init - zsh)"; fi
```

Close and reload the terminal instance

<br/>

## Install ruby-build rbenv-gemset rbenv-whatis rbenv-use

To install RBENV plugins, run the following:

```
mkdir -p "$(rbenv root)"/plugins "$(rbenv root)"/versions &&
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)/plugins/ruby-build" &&
git clone https://github.com/jf/rbenv-gemset.git "$(rbenv root)/plugins/rbenv-gemset" &&
git clone https://github.com/rkh/rbenv-whatis.git "$(rbenv root)/plugins/rbenv-whatis" &&
git clone https://github.com/rkh/rbenv-use.git "$(rbenv root)/plugins/rbenv-use" &&
git clone https://github.com/tpope/rbenv-aliases.git "$(rbenv root)/plugins/rbenv-aliases" &&
rbenv alias --auto
```

<br/>

## Install NVM

NVM documenation is [found here](https://github.com/nvm-sh/nvm#installing-and-updating). To install NVM, run the following:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

Once installed, reload the shell; then run the following:

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

Then

```sh
nvm install --lts && npm install npm@latest -g
```

<br/>

## Install oh-my-zsh

Source found [here](https://ohmyz.sh/)

To install oh-my-zsh, run the following:

```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

<br/>

### Install Oh-My-ZSH Plugins

Run the following:

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions $HOME/.oh-my-zsh/custom/plugins/zsh-autosuggestions &&
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $HOME/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting &&
git clone https://github.com/gusaiani/elixir-oh-my-zsh.git $HOME/.oh-my-zsh/custom/plugins/elixir
```

<br/>

### Install Spaceship-prompt

The [spaceship-prompt](https://github.com/spaceship-prompt/spaceship-prompt) is a clean .oh-my-zsh theme. To install it, run the following:

```sh
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1 && ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$HOME/.oh-my-zsh/themes/spaceship.zsh-theme"
```

<br/>

## Copy the .zshrc Content

Run the following to clear out .zshrc:

```sh
truncate -s 0 .zshrc
```

<br/>

Using VIM or NANO, replace the entire `.zshrc` file with this code:

```zsh
nano .zshrc
```

<br/>

Copy the [contents of .zshrc](ZSHRC.md) and save.

Reload the terminal instance.

<br/>

## Copy .zsh_alias_list Content

Using VIM or NANO, replace the entire `.zsh_alias_list` file with this code:

```zsh
nano .zsh_alias_list
```

<br/>

Copy the [contents of .zsh_alias_list](ZSH_ALIAS_LIST.md) and save.

Reload the terminal instance.

From now on, when you want to reload the shell, simply type `reload`

<br/>

## Copy .zsh_functions

Using VIM or NANO, replace the contents of `.zsh_functions` with the following:

```zsh
nano .zsh_functions
```

<br/>

Copy the [contents of .zsh_functions](ZSH_FUNCTIONS.md) and save.

Type `reload` to reload the shell.

<br/>

## Copy .zsh_jobsauce

This is an example of personal/project content you may needed within console. (You can see how this file is called in [.zshrc](ZSHRC.md))

Using VIM or NANO, replace the contents of `.zsh_jobsauce` with the following:

```zsh
nano .zsh_jobsauce
```

<br/>

Copy the [contents of .zsh_jobsauce](ZSH_JOBSAUCE.md) and save.

Type `reload` to reload the shell.

<br/>

## Copy .gemrc

Using VIM, replace the contents of `.gemrc` with the following:

```zsh
nano .gemrc
```

<br/>

```ruby
---
:backtrace: false
:bulk_threshold: 1000
:sources:
- https://rubygems.org/
:update_sources: true
:verbose: true
install: --no-rdoc --no-ri --no-document
update: --no-rdoc --no-ri --no-document
```

<br>

## Reload

After you have completed the setup, close and reload the terminal instance.

<br/>

## Setup for Ruby and Rails

Setup instructions for Ruby and Rails can be [found here](RUBY_RAILS_SETUP.md)

<br/><br/>

## Setup Systemd (Only if Needed)

This step is onlu need if you plan to run services via Brew and any other service you choose to install and run with Debian. We will need to setup Debian to use `systemd` by following a few simple steps. Info taken from [here](https://devblogs.microsoft.com/commandline/systemd-support-is-now-available-in-wsl/)

*Initially I found that even with the native `systemd` support now available within WSL, that `systemd` and `systemctl` still didn't work as anticipated when enabled. I spent nearly 4 full days looking for the cause and happened upon the answer in an [obscure gihub repo](https://github.com/arkane-systems/bottle-imp#debian) for a utility named `bottle-imp`. The bottle-imp tool was used to provide systemd support for WSL prior to the summer-2022 WSL update, and the bottle-imp code required a list of utilities to be installed for systemd and systemctl to work properly.*

Note: If you use this, systemd removes all content from the `/var/run/` directory when Debian boots up. This means that the `/var/run/postgres` directory gets removed. However, we have a function in `.zshrc` that checks for this dir and creates it. Unfortunately, if the postgres server is running, you will need to restart it. Postges adds the temp file needed by the `PG` gem to connect the rails app to postgres. We also have a couple of functions for that. To stop the postgres server, in the console, call `pgstop`. To start the postgres server, call `pgstart`. This will load the temp file in the in dir. If you would rather just copy the file needed into the dir you can call the following: `pgfix` - this will create link to the tmp file.

<br/>

1. Install the tools that will make systemd and systemctl work as expected:

```bash
sudo apt-get install -y daemonize dbus gawk libc6 policykit-1 python3 python3-pip python3-psutil systemd systemd-container
```
<br/>

2. In the Debian console, run the following:

```bash
sudo nano /etc/wsl.conf
```

<br/>

3. In the nano editor (or use vim, either way), copy the following:

```txt
[boot]
systemd=true
```

<br/>

4. To save the changes, use `ctrl+o` close the file; then hit `y` to save the file; then hit `enter` to close the file.

<br/>

5. Open Windows `Powershell` as an administrator. Type the following:

```powershell
wsl.exe --shutdown
```

<br/>

6. After the Debian instance closes, reopen it and run the following:

```sh
systemctl list-unit-files --type=service
```

You should see a table of info:

![systemctl](https://user-images.githubusercontent.com/516548/201456791-a90c2475-c0e5-4dc8-a113-fc3637cb059e.png)

<br/>

If that doesn't work, I'm not sure what to tell you. WSL changes often and it requires vigilence to keep it working as expected.

<br/><br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-debian.md)
