---
title: "Real-time Rendering Engine Development"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p1_vxgi_reflection.png"
  image: "/assets/images/projects/p1_vxgi_debug.png"
---
We are developing an advanced real-time graphics engine focused on next-generation rendering techniques and GPU optimization. Our research integrates state-of-the-art global illumination algorithms with high-performance DirectX 12 pipeline optimizations to achieve production-quality visual fidelity. The project encompasses both theoretical contributions in real-time rendering and practical engine implementation for modern GPU architectures.

Recent directions include:
1. **Voxel-based Global Illumination (VXGI)**: A 6-level clipmap cascade system with anisotropic radiance storage, diffuse cone tracing, and Jump Flood Algorithm SDF for high-quality specular reflections.
2. **DirectX 12 Engine Optimization**: Systematic integration of frame fence synchronization, custom GPU memory allocators, and resource management strategies adapted from production engines.
3. **Advanced Shadow Rendering**: Real-time shadow catcher plugin development with scene capture and material-based shadow compositing for immersive VR/AR applications.

<figure class="half">
	<img src="/assets/images/projects/p1_vxgi_reflection.png">
	<img src="/assets/images/projects/p1_vxgi_debug.png">
  <figcaption>VXGI reflection results (left) and clipmap debug visualization (right).</figcaption>
</figure>

{% capture programming %}
#### programming experience
C++, DirectX12, HLSL, CUDA, Vulkan
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
