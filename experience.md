---
layout: page
title: 💼 Work Experience
description: A listing of all relevant work experience
nav_order: 2
---

# 💼 Work Experience

{% assign experiences = site.experiences %}
{% for exp in experiences %}
{{ exp }}
{% endfor %}

<!-- {% assign teaching_assistants = site.staffers | where: 'role', 'Teaching Assistant' %}
{% assign num_teaching_assistants = teaching_assistants | size %}
{% if num_teaching_assistants != 0 %}

## Teaching Assistants

{% for staffer in teaching_assistants %}
{{ staffer }}
{% endfor %}
{% endif %} -->