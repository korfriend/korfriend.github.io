---
title: "Dental Realistic Inverse Graphics — DiT × Gaussian Splatting"
permalink: /Projects/dental-inverse-graphics/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p2_hair_dit.png"
  image: "/assets/images/projects/p2_hair_dit.png"
---
We develop a **photorealistic inverse-graphics pipeline for the dental domain**
that combines diffusion-transformer (DiT) priors with 3D Gaussian Splatting (3DGS)
representations and differentiable physically-based rendering. The goal is to
recover crown geometry, material parameters, and scene illumination from
real intra-oral imaging, while *generating* high-fidelity dental textures
that remain consistent across views and lighting conditions.

Recent directions include:
1. **Multi-view Texture Optimization**: A Mitsuba3-based differentiable
   pipeline that fuses DiT-generated texture priors with multi-view
   observations, producing tooth textures that are both globally coherent
   and view-consistent.
2. **Geometry-aware Relighting**: Lighting-aware DiT conditioning that
   disentangles albedo from shading so that generated textures relight
   correctly when re-rendered in arbitrary illumination.
3. **3DGS-based Inverse Graphics**: Linking learned generative priors to
   3DGS scene representations for joint geometry-appearance recovery in
   the dental setting.

<figure>
	<img src="/assets/images/projects/p2_hair_dit.png">
  <figcaption>Diffusion-transformer-driven generation (sample from the lab's DiT pipeline).</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Mitsuba3, Diffusers, 3D Gaussian Splatting frameworks
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
