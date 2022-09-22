---
title: "Goal"
layout: archive
post-order: 1
permalink: categories/comn
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories.Comn %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}