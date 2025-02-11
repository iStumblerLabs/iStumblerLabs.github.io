---
layout: home
---

## Posts

<ul>
  {% for post in site.posts %}
	<li>
	  {{ post.date | date_to_rfc822 }}&nbsp;<a href="{{ post.url }}">{{ post.title }}</a><br>
	  <blockquote>
	  {{ post.excerpt }}
	  </blockquote>
	  <br>
	  <hr>
	</li>
  {% endfor %}
</ul>
