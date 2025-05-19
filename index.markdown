---
layout: home
---

<ul>
  {% for post in site.posts %}
	<h2 style="border: none"><a href="{{ post.url }}">{{ post.title }}</a></h2>
	<code>{{ post.date | date_to_rfc822 }}</code><br>
	<blockquote>{{ post.content | markdownify | strip_html | truncatewords: 50 }}</blockquote>
	<br>
  {% endfor %}
</ul>
