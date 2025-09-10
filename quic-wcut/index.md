---
layout: default
---

# {{ page.dir | remove: '/' | split: '/' | last }}

{% assign current_dir = page.dir %}
{% assign files = site.static_files | where: "extname", ".md" %}
{% assign filtered_files = "" | split: "" %}

{% for file in files %}
  {% if file.path contains current_dir and file.name != "index.md" %}
    {% assign filtered_files = filtered_files | push: file %}
  {% endif %}
{% endfor %}

{% for file in filtered_files %}
- [{{ file.basename }}]({{ file.basename }})
{% endfor %}
