---
layout: page
title: AI 资讯
permalink: /ai/
---

# 🤖 AI 资讯日报

每天早报（07:00）、晚报（19:00）各一期，覆盖 7 个 RSS 源 + 机器之心 + 36氪，只推送真正新的信息，附原文链接。

{% assign ai_posts = site.categories.ai | sort: "date" | reverse %}
{% assign cur = "" %}
{% for post in ai_posts %}
{% assign m = post.date | date: "%Y-%m" %}
{% if m != cur %}
{% assign cur = m %}
## {{ m }}
{% endif %}
- {{ post.date | date: "%m-%d" }} · [{{ post.title }}]({{ post.url }})
{% endfor %}

---

共 **{{ ai_posts.size }}** 期。想看某一期的详情，直接点击标题。
