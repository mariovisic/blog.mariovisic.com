---
layout: post
title: Rails HTTP Streaming
date: 2012-09-06 14:29
comments: true
categories:
- web development
- fast websites
- ruby on rails
---

Rails 3.1 has a feature called HTTP streaming which can speed up the perceived
page load times for your users. It doesn't actually speed anything up, but
rather than waiting for the entire page to be rendered before sending it out,
it starts sending a response as soon as it can.

What this means is that when setup correctly, even if you page renders really
slowly, your app can send the first parts of the page to the end user almost
instantly, and then send the rest as it gets rendered. When the top parts of
the page that contain assets such as CSS then the browser can start downloading
and processing the CSS while it waits for the rest of the page to download.
This can speed up end user page load times dramatically.

<!-- more -->

## Results

Before getting into how to setup HTTP streaming, I thought I'd share the actual
results i've had in a production application. We've been running HTTP streaming
on [Desktoppr](https://www.desktoppr.co/) for the last month or so and here are some charts from NewRelic RPM:

![End user response times](/images/blog/http_streaming/end_user.png)

The purple part of the graph shows time spent waiting for the Web application (which was previously up to
300ms per request), is now effectively gone.

![App server response times](/images/blog/http_streaming/app_server.png)

Here our app server response times don't actually change, rails is reporting
the time it takes to get the first byte out the door, which does dramatically
improves. Previously we were averaging around 150ms for that first byte, now it
takes less than 50ms.

## How to

### Rails

Needs to be 3.1 or newer.

### Templating

You need to use a templating engine that supports HTTP streaming. Currently ERB
and Slim both support HTTP streaming, I have not looked at other templating
engines except for HAML which currently does not support it. 

You will need to move away from HAML if you want to stream, fortunately if you
only want to stream some pages you can just change the layouts + templates +
partials used in that one response, this might save you some time.

`content_for` doesn't play nice with streaming. Instead you can use `provide`
which works the simiarly but only allows you to call it once per yield. Be
careful though as the template will block until the `yield` statement has a
matching `provide` call which may negate the effects of streaming somewhat.

### Rack server

Unicorn supports HTTP streaming with a simple configuration option `tcp_nopush`.
Check the unicorn documentation for more information.

### Controllers

You want to make sure you aren't doing anything intensive in your controllers.
The whole point of streaming is to get as much of the HTML out the door as
quick as possible which means deferring any heavy database calls, any external
calls.

Newer versions of ActiveRecord do not evaluate queries until required, this means that if your code in your controller looks like any of these, then you're all good:

``` ruby
User.limit(10).order('name desc')
User.where(:name => 'BoB')
User.find(5)
```

One thing to look for is when returning a list of results, don't use `.all()` as it will immediately convert the results to an array, use `.scoped()` instead.

``` ruby
# Instead of:
User.all

# Use:
User.scoped
```

### Finally Enabling streaming

You can do this per controller action like so:

``` ruby
class MyController < ActionController::Base
  def show
    render :stream => true
  end
end
```

Or using a responder

``` ruby
class MyController < ActionController::Base
  def show
    @user = User.find(params[:id])
    respond_with @user, :stream => true
  end
end
```

### Rack middleware

### Testing it works

In your views add a sleep maybe somewhere around the closing </head> tag or the opening <body>. Now hit your webpage with curl `curl http://my.local.site/page`.
If working correctly you should notice the top of the page download, then a few seconds later the rest of the page. If it all comes down in one go without sleeping then something is up.
