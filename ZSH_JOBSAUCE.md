[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_jobsauce) | [Customize Ubuntu](customize-ubuntu.md#copy-zsh_jobsauce)

# .zsh_jobsauce

```zsh
#! /bin/zsh

# These aliases and functions assume you have loaded docker things in .zsh_functions

# JOBSAUCE THING   ===============================================================================
JOBSAUCE=$HOME/dev.projects/jobsauce-app
alias js="cd $JOBSAUCE"

# RUN IT LOCALLY - NO DOCKER   ===================================================================
alias jsserv="js && rails s -b 0.0.0.0 -p 3000"
alias jscon="js && rails c"


# JOBSAUCE   ==============================================================================
alias jsf="js && foreman start -f Procfile.dev"
alias jsui="js && foreman start -f Procfile.ui"
alias jss="jsserv"
alias jsc="jscon"
alias jsw="js && yarn build --watch"
alias jscss="js && yarn build:css --watch"
alias jstc="js & open coverage/index.html"

# RUN DB THINGS
alias jsdbc="js && rails db:create db:schema:load db:migrate"
alias jsdbr="js && rails db:drop db:create db:schema:load db:migrate"


# DOCKER =======================================================================================
# alias djsup="js && docker-compose up"
# alias djsz="js && docker exec -it jobsauce-app /bin/zsh"

# alias djsc="js && docker exec -it jobsauce-app /bin/bundle exec rails c"
# alias djss="js && docker-compose up web"
# alias djsw="js && docker-compose up webpacker"

# # RUN DB THINGS
# alias djsdb="js && docker-compose up postgres"
# alias djsdbc="js && docker-compose run --rm web /bin/rails db:create db:schema:load db:migrate"
# alias djsdbr="js && docker-compose run --rm web /bin/rails db:drop db:create db:schema:load db:migrate"

# # RAILS THINGS
# alias djss="js && docker-compose up rails"

function jsinfo () {
  echo ''
  echo '******  JobSauce Settings **************************************'
  echo "JOBSAUCE = $HOME/scott.projects/jobsauce-app"
  echo ''
  echo '******  JobSauce Aliases **************************************'
  echo "js       = cd $JOBSAUCE"
  echo "jsf      = js && foreman start -f Procfile.dev"
  echo "jss      = js && rails s -b 0.0.0.0 -p 3000"
  echo "jsui     = js && foreman start -f Procfile.ui"
  echo "jsw      = js && yarn build --watch"
  echo "jscss    = js && yarn build:css --watch"
  echo "jsc      = js && rails c"
  echo "jstc     = js & open coverage/index.html"
  echo "jsdbc    = js && rails db:create db:schema:load db:migrate"
  echo "jsdbr    = js && rails db:drop db:create db:schema:load db:migrater"
  echo ''
}
alias jsi="jsinfo"
```

<br/><br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Customize Debian](customize-debian.md#copy-zsh_jobsauce) | [Customize Ubuntu](customize-ubuntu.md#copy-zsh_jobsauce)
