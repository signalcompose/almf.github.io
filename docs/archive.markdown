---
layout: default
title: Archive
permalink: /archive/
---

# Archive

## 記事アーカイブ

{% assign postsByYearMonth = site.posts | group_by_exp: "post", "post.date | date: '%Y年%m月'" %}
{% for yearMonth in postsByYearMonth %}
<div style="margin-bottom: 30px;">
  <h3 style="padding: 10px; background: #f5f5f5; border-radius: 4px;">
    {{ yearMonth.name }} ({{ yearMonth.size }}件)
  </h3>
  <div style="padding-left: 20px;">
    {% for post in yearMonth.items %}
    <div style="margin-bottom: 15px; padding-bottom: 15px; border-bottom: 1px solid #eee;">
      <h4 style="margin: 0 0 5px 0;">
        <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none;">{{ post.title }}</a>
      </h4>
      <p style="color: #666; font-size: 14px; margin: 5px 0;">
        {{ post.date | date: "%Y年%m月%d日" }}
      </p>
      <p style="line-height: 1.6; margin: 10px 0;">
        {{ post.content | strip_html | truncate: 150 }}
      </p>
    </div>
    {% endfor %}
  </div>
</div>
{% endfor %}