[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_functions)

<br/>

# .zsh_functions

```zsh
#! /bin/zsh

# function to delete source and local git branch
function gitdel(){
  git push origin --delete $@
  git branch -D $@
  git fetch --all --prune
}

# function update_debian () {
#   echo ''
#   echo 'Updating Debian files, please wait...'
#   sudo bash -c 'for i in update {,dist-}upgrade auto{remove,clean}; do apt-get $i -y; done' &&
#   echo 'Update of Debian complete!'
# }

function upgrade_ohmyzsh(){
  echo ''
  echo 'Updating oh-my-zsh, please wait...'
  omz update &&
  echo "Completed upgrading oh-my-zsh!"
}

function findpg () {
  echo "looking for system 'pg_config'"
  sudo find / -name pg_config
}

function pg_install () {
  echo 'Updating the PG gem'
  gem install pg -- --with-pg-config=/usr/bin/pg_config &&
  echo 'done!'
}
alias pginstall="pg_install"
alias pgi="pg_install"
alias updatepg="pg_install"

function ffi_install () {
  gem install ffi -- --disable-system-libffi
}
alias ffii="ffi_install"

function bundle_install () {
  echo 'Installing gems, please wait...'
  pg_install && ffi_install && bundle
}
alias bi="bundle_install"

function bundle_update () {
  echo 'Updating gems, please wait...'
  pg_install && ffi_install && bundle update
}
alias bu="bundle_update"

function update_rbenv () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating RBENV, please wait...'
  cd "$(rbenv root)" && git pull &&
  cd "$CURR_DIR"
  echo "Done updating RBENV!" &&
  update_ruby_build &&
  update_rbenv_gemset &&
  update_rbenv_whatis &&
  update_rbenv_use &&
  update_rbenv_aliases
}

function update_ruby_build () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating ruby-build, please wait...'
  cd "$(rbenv root)"/plugins/ruby-build && git pull &&
  cd "$CURR_DIR"
  echo "Done updating ruby-build!"
}

function update_rbenv_gemset () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating rbenv-gemset, please wait...'
  cd "$(rbenv root)"/plugins/rbenv-gemset && git pull &&
  cd "$CURR_DIR"
  echo "Done updating rbenv-gemset!"
}

function update_rbenv_whatis () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating rbenv-whatis, please wait...'
  cd "$(rbenv root)"/plugins/rbenv-whatis && git pull &&
  cd "$CURR_DIR"
  echo "Done updating rbenv-whatis!"
}

function update_rbenv_use () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating rbenv-use, please wait...'
  cd "$(rbenv root)"/plugins/rbenv-use && git pull &&
  cd "$CURR_DIR"
  echo "Done updating rbenv-use!"
}

function update_rbenv_aliases () {
  CURR_DIR="$PWD" &&
  echo ""
  echo 'Updating rbenv-aliases, please wait...'
  cd "$(rbenv root)"/plugins/rbenv-aliases && git pull &&
  cd "$CURR_DIR"
  echo "Done updating rbenv-aliases!"
}

function update_brew() {
  echo ''
  echo "Updating BREW"
  ulimit -n 8192 && brew update &&
  echo ''
  echo "Upgrading BREW installs" &&
  ulimit -n 8192 && brew upgrade &&
  echo ''
  echo "Cleaning up BREW" &&
  ulimit -n 8192 && brew cleanup &&
  echo "Completed BREW updates!"
}

function update_nvm() {
  echo "Updating NVM" &&
  (
    cd "$NVM_DIR"
    git fetch --tags origin
    git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
  ) && \. "$NVM_DIR/nvm.sh" &&
  echo "Completed updating NVM!"
}

function upgrade_npm() {
  echo '' &&
  echo "Updating NPM" &&
  npm install npm@latest -g &&
  echo "Completed updating NPM!"
}
alias unpm="upgrade_npm"
alias npmu="upgrade_npm"
alias npm_update="upgrade_npm"
alias npmupdate="upgrade_npm"

function update_omz() {
  echo ''
  # $ZSH/tools/upgrade.sh
  omz update
}

function update() {
  echo "Upgrading ALL the things..."
  update_debian &&
  update_omz &&
  update_rbenv &&
  update_brew &&
  update_nvm &&
  upgrade_npm &&
  echo ''
  echo "All updates complete!!"
}

function cedit () {
  EDITOR="code --wait" bin/rails credentials:edit
}

function fixrails () {
  chmod u+x bin/rails
}
alias railsfix="fixrails"
alias fixr="fixrails"

function bundlei () {
  echo ''
  echo '******  bundle Commands  **************************************'
  echo ''
  echo "pg_install     = gem install pg -- --with-pg-config=/usr/bin/pg_config"
  echo "pgs            = shows pg commands"
  echo ''
  echo "ffi_install    = gem install ffi -- --disable-system-libffi"
  echo "ffii           = ffi_install"
  echo ''
  echo "bundle_install = pg_install && ffi_install && bundle"
  echo "bi             = bundle_install"
  echo ''
  echo "bundle_update  = pg_install && ffi_install && bundle update"
  echo "bu             = bundle_update"
  echo ''
}
alias bundles="bundlei"

function pgs () {
  echo ''
  echo '******  pg Commands  **************************************'
  echo ''
  echo "findpg    = sudo find / -name pg_config   # finds the system pg_config"
  echo "updatepg  = gem install pg -- --with-pg-config=/usr/bin/pg_config"
  echo "upg       = gem install pg -- --with-pg-config=/usr/bin/pg_config"
  echo "pginstall = gem install pg -- --with-pg-config=/usr/bin/pg_config"
  echo ''
  echo "pgstart   = pg_ctl -D /home/linuxbrew/.linuxbrew/var/postgresql@15 start"
  echo "pgstop    = pg_ctl -D /home/linuxbrew/.linuxbrew/var/postgresql@15 stop"
  echo "pgupdate  = brew postgresql-upgrade-database"
  echo ''
}

function updatei () {
  echo ''
  echo '******  Update Commands  **************************************'
  echo ''
  echo "update = update_debian && update_omz && update_rbenv && update_brew && upgrade_npm"
  echo ''
  pgs
  bundles
}
alias updates="updatei"

function ecreds () {
  echo ''
  echo '******  Editing Rails Credentials  **************************************'
  echo 'cedit = EDITOR="code --wait" bin/rails credentials:edit'
  echo 'vedit = EDITOR=vi bin/rails credentials:edit'
}

function gits () {
  echo ''
  echo '****** GIT commands  **************************************'
  echo 'gbr    = git branch'
  echo 'gco    = git checkout'
  echo 'gnew   = git checkout -b'
  echo 'gadd   = git add'
  echo 'gadd.  = git add .'
  echo 'gcom   = git commit -m'
  echo 'gstash = git stash'
  echo 'gpop   = git stash pop'
  echo 'gdrop  = git stash drop'
  echo 'gdel   = git branch -D'
  echo 'godel  = git push origin --delete $1'
  echo 'gfetch = git fetch'
  echo 'gmerge = git merge'
  echo 'gpull  = git pull'
  echo 'gpush  = git push'
  echo 'gstat  = git status'
  echo 'glog   = git log --pretty=full'
  echo 'glogm  = git log --pretty=medium'
  echo ''
}
```

<br/><br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_functions)
