---
layout: post
title: Checking if objects or relations exist in Ruby on Rails
categories:
- ruby
- ruby on rails
- web development
---
I was pair programming with [the great magician Keith](http://keithpitt.com/) yesterday when he pointed out something interesting when checking if objects or relations exist in a collection.

To check if there were any items present in a collection I would do something like this:

``` ruby
object.relation.present?
```

Keith told me to use:

``` ruby
object.relation.any?
```

Turns out that the `any?` method will perform a `COUNT (*)` SQL query where as the
`present?` method will perform a `SELECT (*)` which is infinitely slower than
performing a count.

So from now on i'll be using the `any?` method instead of `present?`