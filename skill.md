---
layout: page
title: ⚙️ Skills
nav_order: 7
---

<p style = "float: right"> 
    <h4 style = "float: right">⚙️ Skills</h4>    
</p>

{% assign skills = site.skills %}
{% for skill in skills %}
    {{ skill }}
{% endfor %}

<hr>

## Miscellaneous

* Jupyter Notebooks
* Git
* Bash
* Docker