---
layout: default
title: Welcome!
---
# Welcome!

Hello there!, let's get to the point, this blog is about finding answers and
cool tips to do your developer life easier. 

# Latest Posts

{% for post in site.posts %}
* ## [{{ post.title }}]({{ post.url }})
  * {{ post.excerpt }}
{% endfor %}
