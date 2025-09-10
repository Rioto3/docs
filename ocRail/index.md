---
layout: default
---

# {{ page.dir | remove: '/' | split: '/' | last }}

{% assign current_dir = page.dir %}
{% assign files = site.static_files | where_exp: "file", "file.path contains current_dir and file.extname == '.md' and file.name != 'index.md'" %}

{% for file in files %}
- [{{ file.basename }}]({{ file.basename }})
{% endfor %}
