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

Rails 3.1 introduced HTTP streaming, a feature that can speed up the perceived
page load times for your users. This feature doesn't actually speed up any of
your code, but rather starts sending the response before the entire page is
rendered.

What this means is that your app can start sending out parts of the page that
do not require any heavy calculation almost immediately. This really helps if
you have some complex actions which take a long time to completely render.

The best part of this feature is that by rendering the top part of the page
quickly, the users browser can begin to download assets such as CSS straight
away, while your application works on getting the rest of the page out the
door. This can speed up end user page load times dramatically.

<!-- more -->

## Results

Before getting into how to setup HTTP streaming, I thought I'd share the actual
results i've had in a production application. We've been running HTTP streaming
on [Desktoppr](https://www.desktoppr.co/) for the last month or so and here are some charts from NewRelic RPM:

![End user response times](/images/blog/http_streaming/end_user.png)

You can see that once streaming was added the purple area drops to almost 0.
The purple area represents time spent waiting for the Web application to
respond (which was previously up to 350ms for our really complex pages).

![App server response times](/images/blog/http_streaming/app_server.png)

Here our app server response times don't actually change, rails is reporting
the time it takes to get the first byte out the door, which does dramatically
improves. Previously our complex pages were taking up to 350ms to render that
first byte, now they take less than 50ms.

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
which works the similarly but only allows you to call it once per yield. Be
careful though as the template will block until the `yield` statement has a
matching `provide` call which may negate the effects of streaming somewhat.

### Rack server

Unicorn supports HTTP streaming with a simple configuration option
`tcp_nopush`. Check the [unicorn
documentation](http://unicorn.bogomips.org/Unicorn/Configurator.html) for more
information. If you're using something besides unicorn then be sure to check
first if it supports streaming.

### Controllers

You want to make sure you aren't doing anything intensive in your controllers.
The whole point of streaming is to get as much of the HTML out the door as
quick as possible which means deferring any heavy database calls, any external
calls.

Newer versions of ActiveRecord do not evaluate queries until it is needed, this means that if your code in your controller looks like any of these, then you're all good:

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

If you have any Rack middleware that modifies your page in some way, then it's
not going to work with streaming unfortunately. Obvious examples of this are
gems that add Google Analytics tracking codes to your page as well as the
newrelic_rpm gem.

To get around this limitation you will need to manually add code for those 3rd
party services to your layout, rather than having middleware tweak your
response. You can disable newrelic auto instrumentation and manually add the
code to your layout as well. [See the newrelic documentation](https://newrelic.com/docs/ruby/real-user-monitoring-in-ruby) 
for more info.

### Testing it works

The first thing to check is that the server isn't calculating a content length and is instead given us a streamed response. You can confirm this by checking the response headers for your site like so:

```
curl -I -X GET http://yourwebsite.com/

# HTTP/1.1 200 OK
# ...
# Transfer-Encoding: chunked
```

If this doesn't show that the transfer encoding is chunked then be sure that
you're running an app server that supports streaming [(perhaps try unicorn)](http://unicorn.bogomips.org/).

Next is the final test, simply add a `sleep(5)` call in your layout, just above
the opening `<body>` tag is usually best. Now curl the page with: `curl
http://your.web.site/`.  If working correctly you should notice the top of the
page download, then a few seconds later the rest of the page. If it all comes
down in one go without pausing then something isn't setup correctly, perhaps
make sure you don't have any rack middleware that is modifying your response.

## More Resources
[Riding Rails announcement](http://weblog.rubyonrails.org/2011/4/18/why-http-streaming/)
[Railscast Episode #266 HTTP Streaming](http://railscasts.com/episodes/266-http-streaming)
