---
layout: default
---

## 最新の記事

{% for post in site.posts %}
<div style="margin-bottom: 40px;">
  <h3 style="margin-bottom: 5px;">
    <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: #267CB9;">{{ post.title }}</a>
  </h3>
  <p style="color: #666; font-size: 14px; margin: 5px 0;">
    {{ post.date | date: "%Y年%m月%d日" }}
  </p>
  <p style="line-height: 1.6;">
    {{ post.content | strip_html | truncate: 200 }}
    <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none;">続きを読む →</a>
  </p>
</div>
{% endfor %}
