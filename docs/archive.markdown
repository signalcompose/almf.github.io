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
    <div style="margin-bottom: 10px;">
      <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none;">{{ post.title }}</a>
      <span style="color: #666; font-size: 14px; margin-left: 10px;">{{ post.date | date: "%m月%d日" }}</span>
    </div>
    {% endfor %}
  </div>
</details>
{% endfor %}

## カテゴリ別アーカイブ

{% assign categories = site.posts | map: "categories" | uniq | sort %}
{% for category in categories %}
  {% if category %}
  <h3>{{ category | capitalize }}</h3>
  <ul style="list-style: none; padding: 0; margin-bottom: 30px;">
    {% for post in site.posts %}
      {% if post.categories contains category %}
      <li style="margin-bottom: 10px;">
        <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none;">{{ post.title }}</a>
        <span style="color: #666; font-size: 14px; margin-left: 10px;">{{ post.date | date: "%Y年%m月%d日" }}</span>
      </li>
      {% endif %}
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}

## すべての記事

<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr style="border-bottom: 2px solid #ddd;">
      <th style="text-align: left; padding: 10px;">タイトル</th>
      <th style="text-align: left; padding: 10px;">日付</th>
      <th style="text-align: left; padding: 10px;">カテゴリ</th>
    </tr>
  </thead>
  <tbody>
    {% for post in site.posts %}
    <tr style="border-bottom: 1px solid #eee;">
      <td style="padding: 10px;">
        <a href="{{ post.url | relative_url }}" style="color: #267CB9; text-decoration: none;">{{ post.title }}</a>
      </td>
      <td style="padding: 10px; color: #666;">{{ post.date | date: "%Y年%m月%d日" }}</td>
      <td style="padding: 10px; color: #666;">{{ post.categories | join: ", " }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>