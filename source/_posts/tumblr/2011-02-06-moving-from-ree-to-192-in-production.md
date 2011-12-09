---
layout: post
title: Moving from REE to 1.9.2 in production
categories:
- ruby
- ruby on rails
- rvm
---
I moved my production box from REE to 1.9.2 today. The process was made very
easy by using _R_V_M. As i&#8217;m using nginx and passenger, I needed to compile
a new copy of nginx with the passenger module included.
Once all done, I benchmarked the knightsarmy site the same way I had done _i_n_ _a_n
_e_a_r_l_i_e_r_ _p_o_s_t. With REE i was hitting 25.07 requests per second. With 1.9.2 I
managed 33.93 per second. Neat!
