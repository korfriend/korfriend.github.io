---
title: "Active Digital Twin via Rig-Constrained 3D Gaussian Splatting"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p5_alignment.png"
  image: "/assets/images/projects/p5_run_summary.png"
---
We are developing an active digital twin framework that combines 3D Gaussian Splatting (3DGS) with uncertainty-driven perception for real-time scene reconstruction and view planning. Our approach integrates multi-camera rig constraints with on-the-fly neural view synthesis, allowing robots to incrementally build accurate digital twins while actively selecting optimal viewpoints for data acquisition.

Recent directions include:
1. **Rig-constrained On-the-fly 3DGS**: Multi-camera rigid-rig integration with streaming 3D Gaussian optimization, reducing per-rig pose estimation from 9×6-DOF to a single 6-DOF body pose while preserving real-time performance.
2. **Medium Reformulation for Volumetric Rendering**: A novel 3DGS formulation that treats Gaussians as participating media rather than surface primitives, enabling more accurate modeling of semi-transparent and volumetric structures.
3. **Active Auxiliary-Sensor Selection**: Uncertainty-aware framework for real-time sensor reliability assessment and active auxiliary view selection, achieving high registration rates with substantial speedup over classic structure-from-motion.

<figure class="half">
	<img src="/assets/images/projects/p5_alignment.png">
	<img src="/assets/images/projects/p5_run_summary.png">
  <figcaption>Trajectory alignment results (left) and multi-view rig run summary (right).</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, Vulkan, custom rasterizer kernels, COLMAP/SfM pipelines
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
