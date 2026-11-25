---
layout: page
title: model gallery
permalink: /gallery/
description: mathematical models and interactive explainers from coursework, research, and self-study
nav: true
nav_order: 4
---

Explore interactive explainers and mathematical models. Click a card to experiment with an idea or read its derivation and results. The notebooks are also on [GitHub](https://github.com/BambooSticker/Model-Gallery).

<div class="projects">
  <div class="row row-cols-1 row-cols-md-3">
    {% assign sorted_models = site.models | sort: "importance" %}
    {% for project in sorted_models %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
</div>
