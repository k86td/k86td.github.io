---
layout: default.liquid
---

Hello! Welcome to my website. I'm Tristan.

## Blog!

{% for post in collections.posts.pages %}
#### {{post.title}}

[{{ post.title }}]({{ post.permalink }})
{% endfor %}

You can also checkout [the test page](testing).
