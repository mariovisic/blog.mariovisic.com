---
layout: post
title: ! 'jQuery: Detecting right click paste on input fields'
categories:
- jQuery
- search
- jQuery search
- web development
---
Today I was creating a jQuery search for a clients website, I wanted the search
to happen once the user types in their search terms without having to press a
search button.
Getting the jQuery action to run once the user changes the input is quite easy:

  $(.search input).keyup(function()
  {
{% endhighlight %}
  });

As you can see from my example I have an input field wrapped inside a div with
class &#8216;search&#8217;. Also my search method is called do_search().
This method works fine for all user keyboard input, including if the user
pastes text into the input using keyboard shortcuts, although it doesn&#8217;t
work if the users pastes text into the input using a right click mouse menu. To
get this behaviour we can bind an action to the paste event like so:

  $(.search input).bind(paste, function()
  {
{% endhighlight %}
  });

This seems to work well, the do_search method is now being called when the user
right click&#8217;s and pastes into our box, although it does have a small
problem. Our code within our action is executed before the actual paste occurs,
this means that our search will be run on whatever is present in the box before
the paste, which is not what we want. To rectify this we can add a small delay
to our do_search method which ensures it is run after the paste is completed.

  $(.search input).bind(paste, function()
  {
{% endhighlight %}
  });

Now with the combination of our actions on the keyup and paste events, the
search should run no matter how the user is putting their search terms into the
input field.
