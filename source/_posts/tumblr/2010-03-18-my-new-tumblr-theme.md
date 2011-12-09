---
layout: post
title: My New tumblr theme.
categories:
- tumblr themes
- web development
- themes
- dev
- html
- css
---
Maybe it&#8217;s because i&#8217;m pedantic? or maybe it&#8217;s because
i&#8217;m a perfectionist? or maybe just because I was bored? I decided to
create my own tumblr theme just for me.
I wasn&#8217;t really satisfied with one of the standard tumblr themes, not
because they aren&#8217;t any good, in fact there was quite a few which were
&#8216;almost just right&#8217; but I kept on thinking &#8220;wouldn&#8217;t it
be better if this was like that instead of how it is&#8221;. As a result I
spent a few hours last night creating my own theme and here it is. I&#8217;ve
even given it a name, CClleeaarr BBlluuee. As you can probably tell, i&#8217;m not a
huge fan of big complex designs, Clear Blue is very minimal but very cclleeaann,
which is how I like it.
Creating the design was fairly straightforward. tumblr provides a really good
guide with lots of information here _h_t_t_p_:_/_/_w_w_w_._t_u_m_b_l_r_._c_o_m_/_d_o_c_s_/_e_n_/
_c_u_s_t_o_m___t_h_e_m_e_s. There was a few little hurdles I ran into so I thought i&#8217;d
run through the process I used in creating my theme.
If you&#8217;re not comfortable playing around with raw HTML and CSS then you
can safely stop reading here, otherwise continue on :)

AAnndd ssoo tthhee tthheemmiinngg pprroocceessss bbeeggiinnss..

The first thing to do is head over to the link above and copy the markup where
it says HHeerree&&##88221177;;ss aann eexxaammppllee ooff tthhee ccoommpplleettee mmaarrkkuupp ffoorr aa tthheemmee. Paste it
into your favourite text editor, for me i&#8217;m using TextMate on my Mac. Now
you&#8217;ll need to figure out what extra features you&#8217;ll want your
design to have. For me I&#8217;ve included the date and tags for each post as
well as extra menu items and the accounts i&#8217;m stalking erm&#8230;
following. If you find you&#8217;re getting stuck at this point, the best thing
to do is go to the customise page in your tumblr account. Once there, select
tthheemmee and then uussee ccuussttoomm HHTTMMLL. This will give you the current themes complete
markup, this will show how the author of another theme has done a particular
item. Have a look through different themes to add features.
So now you&#8217;ll find that we have a lot of markup with tumblr specific
tags. At this point it&#8217;s going to be a bit hard to style anything as we
have no content. What I decided to do was head over to the customize page in my
tumblr account and paste the current markup i&#8217;d been working on into the
current theme and save. Now if we head over to our frontpage we&#8217;ll find
our blog with our current theme applied. There shouldn&#8217;t be any styling
but we need to make sure that all of our features are displaying correctly, so
if you&#8217;ve setup the date of posts and it&#8217;s not appearing then some
fixing may be required. If all the information we want is displaying on the
page then grab a copy of the pages source code and save to a new html file on
your local machine (Normally View ==> Source in your web browser).

NNooww lleettss ddiivvee iinnttoo ssoommee CCSSSS..

Everyone is going to do this step differently so I won&#8217;t go into much
detail. For me i&#8217;ve decided to use the _9_6_0_._g_s_ _C_S_S_ _F_r_a_m_e_w_o_r_k to make
things easier. If you&#8217;re going to be working with external CSS files or
images then you can _uu_pp_ll_oo_aa_dd_ _yy_oo_uu_rr_ _ss_tt_aa_tt_ii_cc_ _ff_ii_ll_ee_ss_ _tt_oo_ _tt_uu_mm_bb_ll_rr which makes it easier to
work with those external files. Once you&#8217;re done styling then paste the
markup back into the custom HTML section of the cuztomize tumblr page.
Lastly comes our variables (which are optional). I decided not to use any
variables at this point as my theme is only for me at the moment. In the future
I might distribute it, although at the moment it remains for me only. Once
again you can find the information for this on the _t_u_m_b_l_r_ _t_h_e_m_i_n_g_ _g_u_i_d_e.
