---
layout: post
title: Things to remember in Vim
categories:
- vim
- programming
- ruby on rails
---
I’ve been using Vim for a couple of months now and soo far it’s been great. I’m still learning new things all the time which is really good as well. Here’s some of the tips and trick’s i’ve picked up

To Automatically indent the current line where it should reside when programming use `==`

Use `Ctrl + c` instead of having to reach for the `ESC` key all the time.

The comment plugin adds the mapping `\c Space` which comments a line (Or multiple visually selected lines). It also uncomments already commented lines.


`:A` to cycle between the test and the implementation (Using the rails plugin).


`:R` to cycle between related files, eg from a view to the controller and back (Using the rails plugin).

`.` Repeats the last action.

`Align [param]` Align the visually selected lines based on the parameter given. So for example `Align =` would align lines based on the equal signs.
