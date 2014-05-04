---
layout: page
title: 试验田
tagline: 种瓜得瓜，种豆得豆
---
{% include JB/setup %}
##早睡早起，锻炼身体

<ul class="posts">
  {% for post in site.posts %}
  <hr>
  <h1>{{post.title}}</h1>
  <p>{{ post.date | date_to_string }}</p>
  
  {{post.description}}
  
  <p><a href="{{ BASE_PATH }}{{ post.url }}">阅读全文</a></p>
  {% endfor %}
  
</ul>

