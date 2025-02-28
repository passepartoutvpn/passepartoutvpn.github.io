---
layout: page
---

## Blog

<ul id="blog-posts">
    {% for post in site.posts %}
    <li>
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <h4>{{ post.date | date: "%b %d, %Y" }}</h4>
    </li>
    {% endfor %}
</ul>
