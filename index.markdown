---
layout: home
---

## Posts

<ul>
  {% for post in site.posts %}
	<li>
	  {{ post.date }}&nbsp;<a href="{{ post.url }}">{{ post.title }}</a>
	</li>
  {% endfor %}
</ul>
