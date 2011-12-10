---
layout: post
title: Simple caching for blog posts.
categories:
- ror
- ruby on rails
- web development
- caching
---
I maintain a website for my local soccer team called [Knights Army](http://www.knightsarmy.net/) which is written in rails3 using a basic blog system I wrote myself. I'm using the
[RedCloth gem](http://rubygems.org/gems/RedCloth) to process textile for blog posts.

The website only gets a very small amount of visitors a day, so performance
isn't a concern of mine at all. The website does feel very snappy when
navigating already. I was looking over the code that I had written a few months
back and noticed that for each post (can be up to 10 shown per page) I was
running RedCloth over the body contents like this:

``` ruby
# app/views/posts/_post.html.haml
= post.body_html
```

``` ruby
# app/models/post.rb
# Yes i realise post is a really bad name for a model
def body_html
  RedCloth.new(self.body).to_html.html_safe
end
```

I had a simple idea to improve the performance of loading the posts. I created
a new text database column called cached_body on the posts table, then added
some logic so that it only runs RedCloth when the post contents change, or when
there is no cached_body already.

``` ruby
# db/migrate/20110109030634_add_cached_body_to_posts.rb
class AddCachedBodyToPosts < ActiveRecord::Migration
  def self.up
    add_column :posts, :cached_body, :text
  end

  def self.down
    remove_column :posts, :cached_body
  end
end
```

```ruby
# app/models/post.rb

before_save :set_cached_body

def body_html
  if cached_body.blank?
    set_cached_body
    save!
  end
  cached_body.html_safe
end

protected

def set_cached_body
  self.cached_body = RedCloth.new(self.body).to_html
end
```

I ran some benchmarks using the [apache benchmark tool](http://httpd.apache.org/docs/2.0/programs/ab.html) for a rough guide of the performance gains. I ran the command `ab -c 100 -n 1000 http://www.knightsarmy.net` a total of 5 times and then took the 3 middle scores to
make an average, here's the results:

``` 
Before:
  Average Time: 57.49 seconds
  Average RPS:  17.40 [#/sec] (mean)

After:
 Average Time:  39.89 seconds
 Average RPS:   25.07 [#/sec] (mean)
```

That's a 44% increase in requests per second and a 30% reduction in
response time. Neat!