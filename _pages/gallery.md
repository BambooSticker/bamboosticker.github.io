---
layout: page
title: model gallery
permalink: /gallery/
description: mathematical models I have built in coursework, research, and self-study, each with its full notebook
nav: true
nav_order: 4
---

All notebooks are on [GitHub](https://github.com/BambooSticker/Model-Gallery). Click a card to read the model, its derivation, and results.

<div class="projects">
  <div class="row row-cols-1 row-cols-md-3">
    {% assign sorted_models = site.models | sort: "importance" %}
    {% for project in sorted_models %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
</div>
