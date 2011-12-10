---
layout: post
title: Fiddling with Prototype
categories:
- jQuery
- javascript
- web development
- prototype
---
Today at work I was exposed to the _P_r_o_t_o_t_y_p_e_ _J_a_v_a_S_c_r_i_p_t_ _f_r_a_m_e_w_o_r_k for the first
time. I've written a fair amount of JavaScript before and recently a lot
of _j_Q_u_e_r_y which is a real pleasure to work with. jQuery is great for a few
reasons. An example is the syntax for all of the methods included is all the
same:

  $(element).method();

So once you get your head around the basic selectors .class and #id then you
can do almost anything instantly. Another great thing about jQuery is the
documentation, the formatting is awesome, easy to find what you want and enough
examples to show you what to do.
Looking at it now, I think it would have been easier to pickup prototype
without having learnt to use jQuery first. I spent my first 10 minutes trying
to find a method similar to jQuerys text() or html() to set the contents of an
element. I almost smacked myself in the head when I realised that the answer in
prototype was innerHtml().
By the end of the day I could defiantly see the purpose of prototype. To me it
feels more like an extension of JavaScript, throwing in helper methods here and
there to make common tasks easy. Although I don't think i'll be
using it over jQuery if given the choice. jQuery has better documentation,
convention and from what I read it's quicker too.
