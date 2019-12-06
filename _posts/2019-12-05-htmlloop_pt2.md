---
layout: single
title: 'Testing HTML loops pt 2'
tags: testing 
---

<div>
<h1> Testing this thing </h1>
{% for file in site.static_files %}
    {% if file.path contains 'html' %}
        <a href="https://danielcaraway.github.io/{{ file.path }}">{{ file.path }}</a>
    {% endif %}
{% endfor %}
</div>