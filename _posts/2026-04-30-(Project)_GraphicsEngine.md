---
title: "Modern In-house Real-time Graphics Engine"
permalink: /Projects/graphics-engine/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p1_vxgi_reflection.png"
  image: "/assets/images/projects/p1_vxgi_debug.png"
---
We develop a modern in-house real-time graphics engine (VizMotive) built on a
contemporary architecture, integrating production-quality rendering features
adapted from state-of-the-art open engines while preserving the flexibility
needed for research-driven extensions. The engine is designed to be the
visualization and rendering backbone for our entire research portfolio —
serving sim-to-real environments, digital-twin reconstruction, and AI-driven
content creation tools developed in the lab.

Recent directions include:
1. **Voxel-based Global Illumination (VXGI)**: A 6-level clipmap cascade with
   anisotropic radiance storage, diffuse cone tracing, and Jump-Flood-Algorithm
   SDF for high-quality specular reflections.
2. **Modern DirectX 12 Pipeline**: Frame-fence synchronization, custom GPU
   memory allocators, and resource-management strategies adapted from modern
   commercial engines for production-grade performance.
3. **Advanced Shadow & Compositing**: Real-time shadow-catcher plugin with
   scene capture and material-based shadow compositing — useful for VR/AR and
   digital-twin overlays.

**Researcher**: [Insung Hwang]({{ '/docs/people/' | relative_url }}) — owns the
modern in-house engine roadmap, from low-level GPU pipeline work to advanced
GI implementations.

<figure class="half">
	<img src="/assets/images/projects/p1_vxgi_reflection.png">
	<img src="/assets/images/projects/p1_vxgi_debug.png">
  <figcaption>VXGI reflection results (left) and clipmap debug visualization (right).</figcaption>
</figure>

{% capture programming %}
#### programming experience
C++, DirectX 12, HLSL, CUDA, Vulkan
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
