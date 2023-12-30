---
layout: page
title: 💻 Projects
description: A listing of all relevant projects
nav_order: 2
---

<p style = "float: right"> 
    <h4 style = "float: right">💻 Projects</h4>    
</p>

{% assign projects = site.projects %}
{% for proj in projects %}
    {{ proj }}
{% endfor %}
