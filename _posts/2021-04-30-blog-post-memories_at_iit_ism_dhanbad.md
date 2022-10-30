---
title: 'Memories at IIT ISM Dhanbad'
date: 2021-04-30
permalink: /posts/2021/04/blog-post-memories-at-IIT-ISM/
tags:
  - cool posts
  - category1
  - category2
---

I am writing this fairly late, after almost 2 years of my graduation. Still things that happened during the college days are just a flashback away, it always seems like yesterday. Some days back, I was scrolling through facebook and stumbled upon this video.
<iframe width="420" height="315" src="../videos/upsanddowns.mp4" frameborder="0"></iframe>

So with this, let's get started with the journey, and I hope you will have certain key takeaways and learnings from the mistakes I made which I have penned down here. 

{% include album.html albumname="college_school" %}

so as to not venture in the paths taken by me 

<div class="home">

  <h1 class="page-heading">Posts</h1>

  <ul class="post-list">
    {% for post in site.posts %}
      {% if post.layout != 'album' %}
        <li>
          <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>

          <h2>
            <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
          </h2>
        </li>
      {% endif %}
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ '../feed.xml' | prepend: site.baseurl }}">via RSS</a></p>

</div>


Headings are cool
======

You can have many headings
======

Aren't headings cool?
------
