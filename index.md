---
title: Chunlin's Blog
layout: page
---

<div id="toc">
    {% for post in site.posts limit: 1 %}
        {% if post.post-link %}
        <h2><center><a href="{{ post.post-link }}" title="External link">{{ post.title }}</a> <a href="{{ post.url }}" title="Permanent link to: '{{ post.title }}'">&raquo;</a></center></h2>
        {% else %}
        <h2><center><a href="{{ site.url }}{{ post.url }}" title="Permanent link to: '{{ post.title }}'">{{ post.title }}</a></center></h2>
        {% endif %}
        {{ post.content }}
        <section class="meta">
         <p id="tip-info">Posted on {{ post.date | date:"%B %e, %Y"}}</p>
</section>
    {% endfor %}
    
    <p>
   <h2> <a href="{{ site.url }}/archive" title="See all posts">SEE ALL POSTS &raquo;</a></h2>
    </p>
</div>
