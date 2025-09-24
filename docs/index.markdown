---
layout: default
---

## 最新の記事

{% for post in site.posts limit:5 %}
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

<div style="text-align: center; margin-top: 40px; padding-top: 20px; border-top: 1px solid #ddd;">
  <a href="{{ "/archive/" | relative_url }}" style="background: #267CB9; color: white; padding: 10px 30px; border-radius: 5px; text-decoration: none; display: inline-block;">
    すべての記事を見る →
  </a>
</div>
