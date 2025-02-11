---
layout: home
---

## Posts

<ul>
  {% for post in site.posts %}
	<li>
	<a href=“{{ post.url }}”>{{ post.title }}</a><br>
	  {{ post.date | date_to_rfc822 }}&nbsp;<br>
	  <blockquote>
	  {{ post.excerpt }}
	  </blockquote>
	  <br>
	  <hr>
	</li>
  {% endfor %}
</ul>
