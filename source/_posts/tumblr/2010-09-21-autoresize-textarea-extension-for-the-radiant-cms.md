---
layout: post
title: Autoresize Textarea extension for the Radiant CMS
tags:
- radiant
- radiant cms
- ruby
- rails
- web development
---
_D_i_r_k_,_ _a_ _c_l_o_s_e_ _f_r_i_e_n_d_ _o_f_ _m_i_n_e had previously modified the radiant CMS so that
all textarea controls in the administration interface would automatically
resize to fit their contents. It was really neat and worked well, although we
both talked about moving it into a radiant extension so that it could easily be
used by others.
Getting started creating radiant extensions is really easy thanks to the
generator that is provided. In a couple of hours, armed with my favourite text
editor and a rubygems.org account the extension was published as a gem and
ready to use. Heres how you go about using it:
Either create or get hold of an existing radiant project. The extension should
work with radiant version 0.9 or greater, then simply run:
gem install radiant-autoresize_textarea-extension
Now add the following line to your config/environment.rb:
config.gem radiant-autoresize_textarea-extension, :lib => false
Now were almost done, we just need to run update on our extension to copy over
the required files.
rake radiant:extensions:autoresize_textarea:update
Also, if I could think of a better name instead of autoresize_textarea I
would have named it something else, add a note with your suggestion if you can
think of one.
