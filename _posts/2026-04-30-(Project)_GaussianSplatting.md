---
title: "3D Gaussian Splatting — Medium Models and Real-time Reconstruction"
permalink: /Projects/gaussian-splatting/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p5_alignment.png"
  image: "/assets/images/projects/p5_run_summary.png"
---
We push **3D Gaussian Splatting (3DGS)** as a unifying scene representation
for both *physically-grounded reconstruction* and *real-time digital twins*.
Our research questions the implicit "thin-surface" assumption of standard
3DGS and develops both more accurate volumetric formulations and faster
incremental reconstruction systems suitable for live capture.

Recent directions include:
1. **Medium-aware 3DGS Reformulation**: Treating Gaussian primitives as
   volumetric *participating media* rather than oriented surface elements,
   yielding more physically meaningful blending — especially for
   semi-transparent and overlapping structures.
2. **Fragment-level Gradient Accumulation**: Forward-pass and gradient
   reformulations that better handle overlapped Gaussians and produce
   sharper optimization signals on hard regions.
3. **High-speed On-the-fly 3DGS**: Rig-constrained streaming reconstruction
   from multi-camera rigs, where the number of pose unknowns is reduced from
   per-camera to per-rig, enabling real-time incremental reconstruction
   with strong robustness over classic SfM pipelines.

<figure class="half">
	<img src="/assets/images/projects/p5_alignment.png">
	<img src="/assets/images/projects/p5_run_summary.png">
  <figcaption>Rig-constrained on-the-fly 3DGS — alignment and run summary.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, Vulkan, custom rasterizer kernels, COLMAP/SfM pipelines
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
