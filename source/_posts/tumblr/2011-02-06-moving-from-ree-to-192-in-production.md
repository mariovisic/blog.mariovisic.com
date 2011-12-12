---
layout: post
comments: true
title: Moving from REE to 1.9.2 in production
categories:
- ruby
- ruby on rails
- rvm
---
I moved my production box from REE to 1.9.2 today. The process was made very
easy by using [RVM](http://beginrescueend.com/). As i'm using nginx and passenger, I needed to compile
a new copy of nginx with the passenger module included.

Once all done, I benchmarked the [knightsarmy](http://www.knightsarmy.net/) site the same way I had done [in an earlier post](http://www.mariovisic.com/post/2674945799/simple-caching-for-blog-posts). With REE i was hitting **25.07 requests per second**. With 1.9.2 I
managed **33.93 per second**. 

Neat!
