---
layout: default
title: Archive
permalink: /archive/
---

# Archive

## 年月別アーカイブ

{% assign postsByYearMonth = site.posts | group_by_exp: "post", "post.date | date: '%Y年%m月'" %}
{% for yearMonth in postsByYearMonth %}
<details style="margin-bottom: 20px;">
  <summary style="cursor: pointer; font-weight: bold; padding: 10px; background: #f5f5f5; border-radius: 4px;">
    {{ yearMonth.name }} ({{ yearMonth.size }}件)
  </summary>
  <div style="padding: 15px;">
    {% for post in yearMonth.items %}
    <div style="margin-bottom: 10px; padding-bottom: 10px; border-bottom: 1px solid #eee;">
      <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none; font-weight: 500;">
        {{ post.title }}
      </a>
      <p style="color: #666; font-size: 14px; margin: 5px 0;">
        {{ post.date | date: "%Y年%m月%d日" }}
      </p>
      <p style="line-height: 1.5; font-size: 14px; color: #333;">
        {{ post.content | strip_html | truncate: 100 }}
      </p>
    </div>
    {% endfor %}
  </div>
</details>
{% endfor %}