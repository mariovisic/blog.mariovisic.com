---
layout: post
title: Ruby 1.9.3rc with RVM
categories:
- ruby
- rvm
---
The Ruby MRI 1.9.3 RC1 has just been released and I wanted to try it out, the
latest version of rvm only lists the 1.9.3 preview1 and 1.9.3-head which
doesn't appear to work correctly. Here's how I managed to get 1.9.3
installed using rvm:

```
 rvm install ruby-1.9.3-tv1_9_3_rc1 --with-libyaml-dir=$HOME/.rvm/usr
 rvm alias create 1.9.3-rc ruby-1.9.3-tv1_9_3_rc1

 rvm use 1.9.3-rc
```

Ruby 1.9.3 works quite well (all of my tests still seem to be green), although
there are a few small issues at the moment. For example ruby-debug19
doesn't currently install.
Running a quick test shows that 1.9.3 does indeed seem to load up a rails
environment much quicker, here is a comparison of running rspec and cucumber
tests for a rails 3.1 project.

```
 Using /Users/mario/.rvm/gems/ruby-1.9.3-tv1_9_3_rc1

 time rspec spec
 Finished in 22.81 seconds

 real  0m28.469s
 user  0m11.000s
 sys   0m0.895s

 time cucumber
 0m4.816s

 real  0m12.955s
 user  0m10.579s
 sys   0m0.701s
```

```
 Using /Users/mario/.rvm/gems/ruby-1.9.2-p290

 time rspec spec
 Finished in 25.69 seconds

 real  0m43.826s
 user  0m18.193s
 sys   0m1.367s

 time cucumber
 0m6.007s

 real  0m24.559s
 user  0m19.324s
 sys   0m1.200s
```

As you can see the actual tests themselves ran faster but not by much, the
total execution time went down a lot though as 1.9.3 has some new fixes to
dramatically speed up the time it takes to require libraries.

## Update

1.9.3rc1 is now available directly through RVM. Simply run:

```
 rvm get head
 rvm reload
 rvm install 1.9.3
```