---
layout: post
title:  "Welcome to Jekyll!"
date:   2017-01-23 17:21:32 +0900
categories: jekyll update
typora-root-url: ..
---
> You’ll find this post in your `_posts` 	 directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.
>

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

```
input{
rabbitmq {
                host => "127.0.0.1"
                queue => "web"
                durable => false
                threads => 1
                prefetch_count => 50
                port => 5672
                user => "guest"
                password => "wpsfldzm21"
        }
 }


filter {
date {
match => [ "time", "UNIX" ]
target => "time_new"
}
}

output {
#       stdout { codec => rubydebug }
        elasticsearch {
                index => "logstash-web-%{+YYYY.MM.dd}"
                hosts => ["192.168.1.22:9200"]
        }
}

```

# asdasssss 

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
