---
title: "Dental Realistic Inverse Graphics"
permalink: /Projects/dental-inverse-graphics/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/dental_dynamics_teaser.jpg"
  image: "/assets/images/projects/dental_dynamics_teaser.jpg"
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
2. **Semantic-aware Photorealistic Inversion**: Recovering rendering
   materials (BRDFs, sub-surface parameters, illumination) from intra-oral
   observations under *semantic guidance* — DiT-driven priors that
   understand structural concepts (e.g., enamel, gum, dentin) so the
   inverse-graphics solver respects material identity rather than only
   matching pixel statistics.
3. **3DGS as a Proxy for Expensive Rendering Kernels**: When the target
   renderer is heavy (e.g., physically-based path tracing), we distill its
   appearance into a 3D Gaussian Splatting representation, enabling fast
   forward and backward passes during inverse-graphics optimization while
   remaining faithful to the underlying physics.
4. **Wild NeRF Alignment with Explicit GS Visibility Optimization**:
   Aligning NeRF reconstructions captured in unconstrained ("in-the-wild")
   conditions and refining them through 3DGS with *explicit visibility*
   terms (per-Gaussian opacity, occluder-aware blending) that make the
   geometry–appearance trade-off interpretable and editable.

<figure>
	<img src="/assets/images/projects/dental_exp.jpg">
  <figcaption>Experimental results from our dental inverse-graphics pipeline — DiT-driven texture priors fused with multi-view differentiable rendering for view-consistent crown appearance recovery.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Mitsuba3, Diffusers, 3D Gaussian Splatting frameworks
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
