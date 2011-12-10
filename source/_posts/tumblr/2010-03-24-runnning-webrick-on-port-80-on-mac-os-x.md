---
layout: post
title: Runnning WEBrick on port 80 on Mac OS X
categories:
- web development
- ruby
- rails
- os x
- mac
---
Due to the security restrictions on OS X, you can't run anything on port
80 without being the superuser. Although running script/server on your rails
application with a sudo prefix won't go down too well as your
environmental variables (gem path, rails environment) won't be set.
To get around this I usually create an alias in which I set my environmental
variables for the sudo command like this:

``` bash
alias server=sudo env RAILS_ENV=development env GEM_PATH=/opt/ruby/gems env
GEM_HOME=/opt/ruby/gems script/server -p 80
``` 

You can add that line to the ~/.profile file in order for it to be set every
time you open the terminal. This will save you having to type it in each time.
