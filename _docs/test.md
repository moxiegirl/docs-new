---
layout: doc
title: TEST
subtitle: Vestibulum ante ipsum primis orci luctus et ultrices posuere cubilia Curae.
---


{% for col in site.collections %}
<p>{{ col.label }}</p>
  {% for doc in col.docs %}
      <p>{{ doc.title }}</p>
  {% endfor %}
{% endfor %}
