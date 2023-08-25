---
title: "Deep Generative Model"
date: 2021-06-01 -0000
categories:
  - Projects
tags:
  - Generative Model
  - AI
  - StyleGAN
  - NeRF

header:
  teaser: "/assets/images/deep_gm_teasor.jpg"
  image: "/assets/images/deep_gm1.jpg"
---
We are currently working on a research project to create new hairstyles using the trained generator of [StyleGAN2](https://github.com/NVlabs/stylegan2). In this research, we are using feature embedding (of various reference images) techniques optimized for a natural style transfer. Specifically, we are trying to find the method for **seamless blending between the naturally generated style image and the original image**. We are also developing an **efficient hairstyle creation solution through various parametric encoding models for interactive style controls using a simple sketche operation**.

We are also conducting research on the improvements of [NeRF](https://github.com/bmild/nerf), a neural network-based scene representation model, specifically for **few-shot cases and dynamic scene cases**. The researching features will be added to the NeRF plugin module of the rendering engine that our laboratory has been developing.

{% capture programming %}
#### programming experience
Python, Pytorch, Python
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>