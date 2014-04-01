---
layout: page
title:  
tagline: 
---
{% include JB/setup %}


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; 
	<h2><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
	<p class="postlistexcerpt">{{ post.content | strip_html | truncatewords:50 }}</p>
	<hr/>
	</li>
  {% endfor %}
</ul>
