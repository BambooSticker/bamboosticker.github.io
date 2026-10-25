---
layout: page
title: "Benders decomposition for MPC"
description: "a one-dimensional, one-step MPC solved by generalized Benders decomposition"
img: assets/img/gallery/benders_mpc.jpg
importance: 1
github: https://github.com/BambooSticker/Model-Gallery/blob/main/benders_mpc.ipynb
---

**Language:** Python · **Source:** [`benders_mpc.ipynb`](https://github.com/BambooSticker/Model-Gallery/blob/main/benders_mpc.ipynb) on GitHub · [all models](/gallery/)

A minimal model predictive control problem that shows, step by step, how generalized Benders decomposition builds a piecewise-affine approximation of the value function with cuts, and how initialization changes convergence.

{::nomarkdown}
{% assign jupyter_path = "assets/jupyter/gallery/benders_mpc.ipynb" | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}
