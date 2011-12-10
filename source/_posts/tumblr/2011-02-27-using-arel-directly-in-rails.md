---
layout: post
title: Using arel directly in rails
categories:
- ruby on rails
- web development
- arel
---
Today I was creating a model method which would return some associated objects.
It wasn't hugely complex but I basically needed to match an sql string
which looked something like this:

  SELECT * FROM table WHERE column_one = something AND column_two = something
  OR column_three = something AND column_four = something

After reading some arel documentation, I came up this:

  version  = Version.arel_table
  versions = Version.where(version[:c1].eq(something).and(version[:c2].eq
  (something)).or(version[:c3].eq(something).and(version[:c4].eq(something))))

If this is a bit too fiddly for you then there are some nice gems that do this
for you, such as _M_e_t_a_ _W_h_e_r_e.
