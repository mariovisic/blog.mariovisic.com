---
layout: post
title: Some fun with git
tags:
- git
- source code control
- awesome
---
Found a neat trick today while trying to figure out something in git:
I had a folder in my project which i wanted to be ignored and not tracked by
git, the folder was called site, so my gitignore file had the following line:
site/*
Although today i realised there was a subfolder called javascript which i
wanted to track, but still ignore the rest of site. Instead of manually
setting ignore for each of the folders and files within site i googled around a
bit and came up with this:
site/*
!site/javascripts
This ignores all of the files and subfolders in site except for javascripts.
I love git :) Also I wasnt sure if the author of this post was kidding, or
serious ? _h_t_t_p_:_/_/_s_t_a_c_k_o_v_e_r_f_l_o_w_._c_o_m_/_q_u_e_s_t_i_o_n_s_/_7_6_7_1_4_7_/_h_o_w_-_d_o_-_i_-_t_e_l_l_-_g_i_t_-_t_o_-
_i_g_n_o_r_e_-_g_i_t_i_g_n_o_r_e
