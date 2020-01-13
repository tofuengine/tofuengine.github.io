---
title: docs
caption: docs
layout: home
permalink: /docs/
---

# Lorem ipsum

<ol>
{% for page in site.docs %}
    {% if page.category == "docs" %}
        <li><a href="{{ page.url }}">{{ page.title }}</a></li>
    {% endif %}
{% endfor %}
</ol>
