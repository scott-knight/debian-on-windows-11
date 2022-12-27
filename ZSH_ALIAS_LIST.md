[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_alias_list-content)

<br/>

# .zsh_alias_list

```zsh
#! /bin/zsh

# SYSTEM
alias ll='ls -FlaG'
alias reload='omz reload'
alias home='cd ~'
alias dls="cd ~/Downloads"
alias myip="curl https://ipecho.net/plain; echo"
alias ehosts="sudo vim /private/etc/hosts"
alias pbcopy="clip.exe"
alias pbpaste="powershell.exe -command 'Get-Clipboard' | head -n -1"


# Projects code
PROJCS=$HOME/dev.projects
alias dev="cd $PROJCS && ll"
alias sdev="dev"
alias sui="cd $PROJCS/sandbox-js"
alias sjs="sui"
alias sapi="cd $PROJCS/sandbox-api"
alias c="code"


# ERLANG
alias erlang="echo Erlang version is: ; erl -eval 'erlang:display(erlang:system_info(otp_release)), halt().'  -noshell ; echo use the command erl to start the Erlang CLI"


# Ruby/Rails
alias echomigrate="echo Performing rails migration"
alias echotestmigration="echo Performing rails migration for Test"
alias migrate="echomigrate ; rake db:migrate"
alias migratetest="echotestmigration ; RAILS_ENV=test bundle exec rake db:migrate"
alias rollback="echo Performing rollback... ; bundle exec rake db:rollback"
alias rnew="echo rails new <app_name> --webpack --skip-turbolinks --skip-spring --skip-coffee -T -B -d postgresql"
alias mkenvs="touch .ruby-version ; touch .ruby-gemset"
alias vedit='EDITOR=vi bin/rails credentials:edit'
alias rslh="rails s -b 0.0.0.0 -p $1"
alias rc='rails c'
alias rg='rails g'
alias rfix="chmod u+x bin/rails"


# GIT commands
alias gbr="git branch "
alias gco="git checkout "
alias gnew="git checkout -b "
alias gadd="git add"
alias gadd.="git add ."
alias gcom="git commit -m"
alias gstash="git stash"
alias gpop="git stash pop"
alias gdrop="git stash drop"
alias gdel="git branch -D "
alias godel="git push origin --delete $1"
alias gfetch="git fetch"
alias gmerge="git merge"
alias gpull="git pull"
alias gpush="git push"
alias gstat="git status"
alias glog="git log --pretty=full"
alias glogm="git log --pretty=medium"


# rbenv list
alias rbv="rbenv version"                        # shows the current ruby version
alias rbvs="rbenv versions"                      # shows installed ruby versions
alias rbvlist="rbenv install --list-all"         # show all availabe ruby versions
alias rehash="rbenv rehash"                      # refreshes rbenv
alias active="rbenv gemset active"               # shows the active gemset
alias gemsloc="gem env home"                     # shows the current rubygems environment
alias gemloc="gem env home"                      # shows the current rubygems environment
alias gemenv="gem env home"                      # shows the current rubygems environment
alias gsi="rbenv gemset init \$1"                # allows you to create and set a gemset, ex: gsi rails5x
alias gsc="rbenv gemset create \$(ruby_ver) \$1" # allows you to create a gemset, ex: gsc rails5x
alias gsd="rbenv gemset delete \$(ruby_ver) \$1" # allows you to delete a gemset, ex: gsd rails5x
alias gsadd="echo -e > .ruby-gemset"             # creates a generic gemset file
alias rubyadd="echo \$1 > .ruby-version"         # allows you to set the desired ruby version, ex: rubyadd 2.3.1
alias rmgems='echo Removing .rbenv-gemsets ; rm -rf .rbenv-gemsets'
alias rbvdoc='curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash'

# nvm
alias nvms="nvm list"
alias nvmlist="nvm ls-remote"

# Yarn
alias yup="yarn upgrade --latest"
alias yupdate="yup"
alias ylist="yarn list"
alias yl="ylist"
alias ylg="ylist | grep $1"
alias ydev="yarn dev"

alias pgstart="pg_ctl -D /home/linuxbrew/.linuxbrew/var/postgresql@15 start"
alias pgstop="pg_ctl -D /home/linuxbrew/.linuxbrew/var/postgresql@15 stop"
alias pgupdate="brew postgresql-upgrade-database"

alias python="$(brew --prefix python)"
```
<br/><br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_alias_list-content)
