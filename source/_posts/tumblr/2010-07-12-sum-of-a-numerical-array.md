---
layout: post
title: Sum of a numerical array
categories:
- ruby
- rails
- web development
- beautiful
- code
---
Found a neat little ruby code snippet (below) to get the total sum of an array full of numbers.
I needed it for one of the [Project Euler](http://projecteuler.net/) problems!

``` ruby
sum = array.inject(:+)
```
