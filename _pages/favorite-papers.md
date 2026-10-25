---
layout: page
permalink: /favorite-papers/
title: favorite papers
description: papers I keep coming back to
nav: true
nav_order: 5
---

<!-- Entries live in _bibliography/favorites.bib; the keywords field picks the section. -->

<div class="publications">

<h2>optimization</h2>
{% bibliography --file favorites --query @*[keywords~=optimization] --group_by none %}

<h2>machine learning</h2>
{% bibliography --file favorites --query @*[keywords~=learning] --group_by none %}

<h2>control</h2>
{% bibliography --file favorites --query @*[keywords~=control] --group_by none %}

</div>
