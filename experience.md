---
layout: page
title: 💼 Work Experience
description: A listing of all relevant work experience
nav_order: 1
---

<p style = "float: right"> 
    <h4 style = "float: right">💼 Work Experience</h4>    
</p>

{% assign experiences = site.experiences %}
{% for exp in experiences %}
    <div> <a href="#{{exp.section}}"></a> </div>
    {{ exp }}
{% endfor %}
