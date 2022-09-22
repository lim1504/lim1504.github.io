---
title: "Goal"
layout: archive
permalink: categories/comn
author_profile: true
sidebar_main: true
categories: [categories]
---


{% assign posts = site.categories.comn %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}