---
title: "Generative AI for 3D Content Creation and Editing"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p2_hair_dit.png"
  image: "/assets/images/projects/p2_hair_dit.png"
---
We focus on developing novel generative AI techniques for high-quality 3D content creation and precise editing. Our research spans diffusion transformer (DiT) architectures for controllable hair generation and neural texture synthesis pipelines for photorealistic dental modeling, pushing the boundaries of generative models in specialized computer graphics domains.

Recent directions include:
1. **Hair-DiT**: Sketch-guided hair inpainting using a matte-gated ControlNet architecture on diffusion transformers, enabling realistic and context-robust hairstyle generation and editing.
2. **Neural Dental Texturing**: Multi-view texture optimization combining differentiable rendering (Mitsuba3) with geometry-aware relighting for photorealistic dental crown synthesis.
3. **3D-Aware Generation**: Context-robust generation techniques that maintain multi-view consistency and spatial coherence in diffusion-based 3D content creation.

<figure>
	<img src="/assets/images/projects/p2_hair_dit.png">
  <figcaption>Sketch-guided hair generation result from our Hair-DiT pipeline.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Diffusers, Mitsuba3, ControlNet/DiT frameworks
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
