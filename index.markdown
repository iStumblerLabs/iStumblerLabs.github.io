---
layout: home
---

## Posts

<ul>
  {% for post in site.posts %}
	<h5>({{ post.title }})[{{ post.url }}]</h5>
	<code>{{ post.date | date_to_rfc822 }}<code><br>
	<blockquote>{{ post.excerpt }}</blockquote>
	<br>
	<hr>
  {% endfor %}
</ul>
