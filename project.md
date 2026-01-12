---
layout: page
title: 💻 Projects
description: A listing of all relevant projects
nav_order: 3
---

<p style = "float: right"> 
    <h4 style = "float: right">💻 Projects</h4>    
</p>
<br>
See below for descriptions and the skills and technologies used for my Data Science projects. To see associated code and get a more in-depth description of the work done for each project, navigate to the GitHub repositories for each. 

{% assign projects = site.projects %}
{% for proj in projects %}
    {{ proj }}
{% endfor %}
