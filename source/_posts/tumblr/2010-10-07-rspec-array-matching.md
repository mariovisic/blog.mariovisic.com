---
layout: post
title: Rspec Array Matching
categories:
- rails
- rspec
- testing
---
I started my new job today, for the first day they paired me with _o_n_e_ _o_f_ _m_y
_f_r_i_e_n_d_s who I knew before getting the position.
We were creating some tests for a method which returned an array of objects, we
knew the objects that would come out but it was hard to get them in the right
order. Trying to match the two arrays didn&#8217;t work:

  @result.should == @expected_array

We didn&#8217;t want to simply sort both arrays as the test would get longer
and we shouldn&#8217;t really have to, so after poking around a bit we (well
mostly Darcy) discovered that rspec provides the ~~== matcher to match an array
for any given order. So this works flawlessly

  @result.should =~ @expected_array

:)
