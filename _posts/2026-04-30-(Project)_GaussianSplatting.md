---
title: "3D Gaussian Splatting — Explicit Worlds and Real-time Reconstruction"
permalink: /Projects/gaussian-splatting/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/gs_surround_rig.jpg"
  image: "/assets/images/projects/gs_surround_rig.jpg"
---
We push **3D Gaussian Splatting (3DGS)** as a unifying scene representation for
both *physically-grounded reconstruction* and *real-time digital twins*. Two
questions drive the work. First, whether the implicit "thin-surface"
assumption behind standard 3DGS should be replaced by a genuinely volumetric
formulation. Second, whether a scene can be reconstructed *while it is being
observed* — incrementally, from a moving multi-camera rig, fast enough to be
used as a live map rather than an offline artifact.

Recent directions include:

1. **Medium-aware 3DGS Reformulation**: Treating Gaussian primitives as
   volumetric *participating media* rather than oriented surface elements,
   yielding more physically meaningful blending — especially for
   semi-transparent and overlapping structures.

2. **Fragment-level Gradient Accumulation**: Forward-pass and gradient
   reformulations that better handle overlapped Gaussians and produce sharper
   optimization signals on hard regions.

3. **On-the-fly Reconstruction**: Instead of optimizing a whole captured
   sequence at once, the map is bootstrapped once and then updated per frame:
   the incoming view is posed against the current map, new Gaussians are
   introduced only where the render-versus-image residual and a reliable depth
   estimate agree that geometry is missing, a lightweight single-view step
   corrects the position, colour, scale and opacity of the existing map, and
   redundant Gaussians are pruned to keep memory and compute bounded. No
   re-optimization of the full sequence is required.

4. **Omnidirectional (Equirectangular-native) Reconstruction**: Driving needs
   the sides and the rear as much as the front, and a wide field of view breaks
   the pinhole assumptions the standard pipeline is built on. We reformulate
   the incremental pipeline natively on the sphere — pixels become direction
   vectors, camera *z*-depth becomes radial range, reprojection error in pixels
   becomes angular error between rays, with the corresponding spherical
   Jacobian, longitude seam continuity and latitude weighting.

<figure>
	<img src="/assets/images/projects/gs_eqr_otf.jpg">
  <figcaption>Equirectangular input and the radial range used to seed and correct Gaussians. Working in radial range rather than camera z-depth keeps the geometry consistent across the full 360° field of view.</figcaption>
</figure>

5. **Rig-constrained Multi-camera Reconstruction**: Four fisheye cameras are
   rigidly mounted on the vehicle body, so their relative poses are fixed and
   known. The unknowns collapse from one pose per camera to a single body pose
   per time step, and all four views update one shared Gaussian map
   simultaneously — a much better conditioned problem than posing each camera
   independently, and considerably more robust than classic structure-from-motion
   on this kind of low-overlap, wide-baseline rig.

6. **Interactive Surround View**: From that shared map the scene can be viewed
   from anywhere — top view, quarter view, or a free trajectory. This is where
   the explicit 3D representation pays off against the standard approach:
   inverse-perspective mapping re-projects the camera images onto a single
   ground plane, so anything with height is smeared, whereas the reconstructed
   map keeps height and lets an obstacle retain its shape from an arbitrary
   viewpoint.

<figure>
	<img src="/assets/images/projects/gs_ipm_vs_gs.jpg">
  <figcaption>The same parked scene under inverse-perspective mapping (left) and 3DGS reconstruction (right). Planar re-projection collapses the neighbouring vehicle into a smear on the ground; the reconstructed map preserves its height and outline.</figcaption>
</figure>

<figure>
	<img src="/assets/images/projects/gs_topview_strip.jpg">
  <figcaption>Top view of the same scene, left to right: ground truth, inverse-perspective mapping, offline 3DGS, and on-the-fly incremental 3DGS.</figcaption>
</figure>

7. **Generative Scene Compilation**: A longer-term direction is to treat
   generative models as a *scene compiler* — distilling the geometric and
   appearance priors of large image and video diffusion models directly into
   explicit 3DGS parameters, with objects separated from the background. The
   point is not to generate pictures of a scene but to obtain an explicit,
   physics-ready world that a simulator can then run.

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, Vulkan, custom rasterizer kernels, spherical camera
models, incremental pose estimation, COLMAP/SfM pipelines
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
