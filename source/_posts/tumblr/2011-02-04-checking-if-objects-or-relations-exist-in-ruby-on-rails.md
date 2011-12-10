---
layout: post
title: Checking if objects or relations exist in Ruby on Rails
categories:
- web development
- ruby on rails
- programming
---
I was pair programming with _t_h_e_ _g_r_e_a_t_ _m_a_g_i_c_i_a_n_ _K_e_i_t_h yesterday when he pointed
out something interesting when checking if objects or relations exist in a
collection.
To check if there were any items present in a collection I would do something
like this:

  Object.relation.present?

Keith told me to use:

  Object.relation.any?

Turns out that the aannyy?? method will perform a CCOOUUNNTT ((**)) SQL query where as the
pprreesseenntt?? method will perform a SSEELLEECCTT ((**)) which is infinitely slower than
performing a count.
So from now on i'll be using the any? method instead of present?
