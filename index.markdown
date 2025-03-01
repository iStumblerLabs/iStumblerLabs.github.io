---
layout: home
---

## Posts

<ul>
  {% for post in site.posts %}
	<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
	<code>{{ post.date | date_to_rfc822 }}<code><br>
	<blockquote>{{ post.excerpt }}</blockquote>
	<br>
	<hr>
  {% endfor %}
</ul>
