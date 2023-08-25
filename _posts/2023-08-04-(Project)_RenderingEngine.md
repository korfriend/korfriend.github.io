---
title: "Rendering and Visualization"
date: 2021-02-01 -0000
categories:
  - Projects
tags:
  - Scientific and Medical Visualization
  - Photorealistic Rendering
  - Volume Rendering
header:
  teaser: "/assets/images/rendering_and_vis_teasor.jpg"
  image: "/assets/images/rendering_and_vis_plan.gif"
---
We have been developing our own rendering engine for over 10 years since 2010, and have extensive experience in successfully applying it to commercial visualization solutions. Based on a deep understanding of high-level graphics libraries like Three.js and Unreal Engine, we specialize in creating a customized/multi-modal visualization engine, which includes efficient rendering pipelines, specialized data structures, and resource management.
Recently, we have been working on 
1. the commercial SW development toolkit based on our graphics engine for dental/medical visualization solutions,  
2. the development of a plugin module to support scene composition and rendering based on [instant NeRF](https://github.com/NVlabs/instant-ngp), and 
3. the development of a WebGPU-based web support engine wrapper.
In particular, the [NeRF](https://github.com/bmild/nerf) plugin module will be used as a base for future NeRF-related technological research in our laboratory.

<figure>
	<img src="/assets/images/rendering_and_vis1.jpg">
  <figcaption>basic features of our rendering engine.</figcaption>
</figure>

{% capture programming %}
#### programming experience
C++, DirectX, Cuda, Pytorch, Tensorflow, Python, Javascript
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>