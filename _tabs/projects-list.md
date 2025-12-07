---
layout: page
title: Projects
icon: fas fa-folder-open
order: 2
---

# Portfolio Projects

Below is an automatically updated list of projects synced from Notion.

<ul>
{% for file in site.static_files %}
  {% if file.path contains '/projects/' and file.extname == '.md' %}
    <li>
      <a href="{{ file.path | relative_url }}">{{ file.name | replace: '.md', '' }}</a>
    </li>
  {% endif %}
{% endfor %}
</ul>
