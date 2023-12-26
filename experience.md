---
layout: page
title: 💼 Work Experience
description: A listing of all relevant work experience
nav_order: 1
has_children: true
has_toc: false
---

<p style = "float: right"> 
    💼 Work Experience    
</p>

{% assign experiences = site.experiences %}
{% for exp in experiences %}
    {{ exp }}
{% endfor %}
