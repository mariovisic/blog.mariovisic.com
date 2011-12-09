---
layout: post
title: Setup radiant projects easily with radiant-go
tags:
- radiant
- radiant-go
- ruby
- rails
- web development
---
Recently I began work on a project called radiant-go. Radiant-go is a rubygem
that allows you to setup radiant projects easily. It saves a huge amount of
time when setting up applications and its very easy to configure.
Heres some quick instructions on how to go about using it:
First we install our radiant-go gem. It depends on radiant and bundler so it
will install those too if they arent installed yet.
gem install radiant-go
Now we can generate our configuration files and modify them to our needs. This
step is only necessary if you want to modify the initial configuration of your
application.
radiant-go -c project
Now we can run our generator. If you have followed the step above, you need to
run the generator on the same folder.
radiant-go project
TThhaattss aallll,, wweerree ddoonnee.. Your Radiant install is ready to use.
