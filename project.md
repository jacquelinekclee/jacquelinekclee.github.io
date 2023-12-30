---
layout: page
title: 💻 Projects
description: A listing of all relevant projects
nav_order: 2
---

<p style = "float: right"> 
    <h4 style = "float: right">💻 Projects</h4>    
</p>

<p> test </p>

{% assign projects = site.projects %}
{% for proj in projects %}
    <p> test2 </p>
    {{ proj }}
{% endfor %}
