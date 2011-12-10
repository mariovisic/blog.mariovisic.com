---
layout: post
title: My New tumblr theme
categories:
- tumblr
- web development
---
Maybe it’s because i’m pedantic? or maybe it’s because i’m a perfectionist? or maybe just because I was bored? I decided to create my own tumblr theme just for me.

I wasn’t really satisfied with one of the standard tumblr themes, not because they aren’t any good, in fact there was quite a few which were ‘almost just right’ but I kept on thinking "wouldn’t it be better if this was like that instead of how it is". As a result I spent a few hours last night creating my own theme and here it is. I’ve even given it a name, **Clear Blue**. As you can probably tell, i’m not a huge fan of big complex designs, Clear Blue is very minimal but very clean, which is how I like it.

Creating the design was fairly straightforward. tumblr provides a really good guide with lots of information here [http://www.tumblr.com/docs/en/custom_themes](http://www.tumblr.com/docs/en/custom_themes). There was a few little hurdles I ran into so I thought i’d run through the process I used in creating my theme.

If you’re not comfortable playing around with raw HTML and CSS then you can safely stop reading here, otherwise continue on :)

And so the theming process begins.

The first thing to do is head over to the link above and copy the markup where it says **Here’s an example of the complete markup for a theme**. Paste it into your favourite text editor, for me i’m using TextMate on my Mac. Now you’ll need to figure out what extra features you’ll want your design to have. For me I’ve included the date and tags for each post as well as extra menu items and the accounts i’m stalking erm… following. If you find you’re getting stuck at this point, the best thing to do is go to the customise page in your tumblr account. Once there, select **theme** and then **use custom HTML**. This will give you the current themes complete markup, this will show how the author of another theme has done a particular item. Have a look through different themes to add features.

So now you’ll find that we have a lot of markup with tumblr specific tags. At this point it’s going to be a bit hard to style anything as we have no content. What I decided to do was head over to the customise page in my tumblr account and paste the current markup i’d been working on into the current theme and save. Now if we head over to our frontpage we’ll find our blog with our current theme applied. There shouldn’t be any styling but we need to make sure that all of our features are displaying correctly, so if you’ve setup the date of posts and it’s not appearing then some fixing may be required. If all the information we want is displaying on the page then grab a copy of the pages source code and save to a new html file on your local machine (Normally View ==> Source in your web browser).

### Now lets dive into some CSS.

Everyone is going to do this step differently so I won’t go into much detail. For me i’ve decided to use the [960.gs CSS Framework](http://960.gs/) to make things easier. If you’re going to be working with external CSS files or images then you can [upload your static files to tumblr](http://www.tumblr.com/themes/upload_static_file) which makes it easier to work with those external files. Once you’re done styling then paste the markup back into the custom HTML section of the customise tumblr page.

Lastly comes our variables (which are optional). I decided not to use any variables at this point as my theme is only for me at the moment. In the future I might distribute it, although at the moment it remains for me only. Once again you can find the information for this on the [tumblr theming guide](http://www.tumblr.com/docs/en/custom_themes#custom-colors).