---
layout: page
title: 💼 Work Experience
description: A listing of all relevant work experience
nav_order: 1
---

<p style = "float: right"> 
    💼 Work Experience    
</p>

{% assign experiences = site.experiences %}
{% for exp in experiences %}
    {{ exp }}
{% endfor %}
