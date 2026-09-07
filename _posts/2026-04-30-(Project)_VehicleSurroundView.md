---
title: "On-the-fly Gaussian Splatting for Vehicle Surround View"
permalink: /Projects/vehicle-surround-view/
date: 2026-04-30 -0000
published: true
categories:
  - Projects
header:
  teaser: "/assets/images/projects/gs_surround_rig.jpg"
  image: "/assets/images/projects/gs_surround_rig.jpg"
---
We are building a **surround view for vehicles on top of an explicit 3D scene
representation**. Four fisheye cameras are mounted on the vehicle body — front,
rear, left and right — and the scene around the car is reconstructed as **3D
Gaussians while the car is driving**, rather than being optimised offline after
the sequence has been captured. The target scenario is low-speed manoeuvring in
underground parking structures, where the driver needs to see what is beside and
behind the car, and where the objects that matter — pillars, kerbs, neighbouring
vehicles — all have height.

### Why the standard surround view is not enough

Production around-view monitors are built on **inverse-perspective mapping
(IPM)**: the four camera images are re-projected onto a single ground plane and
stitched. That assumption is exact only for the road surface. Anything standing
above the ground — a pillar, an open door, an adjacent car — is projected as if
it were painted flat, so it is stretched along the viewing direction and appears
to lie down on the floor. It is also a fixed product: because there is no 3D
structure behind it, the composite can only ever be shown from the one virtual
viewpoint the homography was built for.

<figure>
	<img src="/assets/images/projects/gs_ipm_vs_gs.jpg">
  <figcaption>The same parked scene under inverse-perspective mapping (left) and 3D Gaussian Splatting reconstruction (right). Planar re-projection collapses the neighbouring vehicle into a smear on the ground; the reconstructed map preserves its height and outline.</figcaption>
</figure>

An explicit 3D map removes that assumption. The question we work on is whether
such a map can be produced **fast enough to be used while driving**, from a
camera rig that is wide-angle, low-overlap and rigidly fixed to a moving body.

### Approach

**On-the-fly incremental reconstruction.** Instead of optimising a whole
captured sequence at once, the map is bootstrapped once and then updated per
frame: the incoming view is posed against the current map, new Gaussians are
introduced only where the render-versus-image residual and a depth estimate
agree that geometry is missing, a lightweight optimisation step corrects the
position, colour, scale and opacity of the existing map, and redundant Gaussians
are removed to keep memory and compute bounded. No re-optimisation of the full
sequence is required.

**Wide field of view handled natively.** A fisheye lens breaks the pinhole
assumptions the standard pipeline is built on, and converting to perspective
images throws away exactly the peripheral field of view that a surround view
needs. We therefore keep the spherical geometry throughout: pixels are treated
as direction vectors, camera *z*-depth becomes radial range, and reprojection
error in pixels becomes angular error between rays, with the corresponding
spherical Jacobian and latitude weighting. The same reformulation was first
validated on equirectangular 360° input before being carried over to the
vehicle's fisheye rig.

<figure>
	<img src="/assets/images/projects/gs_eqr_otf.jpg">
  <figcaption>Omnidirectional input and the radial range used to seed and correct Gaussians. Working in radial range rather than camera z-depth keeps the geometry consistent across the full field of view.</figcaption>
</figure>

**Rig constraints instead of free-form structure-from-motion.** The four cameras
are bolted to the body, so their relative poses are fixed and known. The unknowns
collapse from one pose per camera to a single body pose per time step, and all
four views update one shared Gaussian map simultaneously. This is a much better
conditioned problem than posing each camera independently, and considerably more
robust than classic structure-from-motion on a rig with this little overlap
between neighbouring cameras — under two metres from the car, adjacent fisheye
views share only a few percent of their visible surface.

**Improving the representation underneath.** Running alongside this system is a
separate line of work on the Gaussian representation itself: treating primitives
as volumetric participating media rather than oriented surface elements, and
reformulating gradient accumulation at the fragment level so that heavily
overlapped Gaussians produce a sharper optimisation signal. Both matter directly
for a driving rig, which observes surfaces at grazing angles through long stacks
of overlapping primitives — precisely the regime where the standard formulation
is weakest. Gains there raise the ceiling for everything described above, and the
work is pursued on its own rather than as part of this pipeline.

### Where the work stands

On synthetic underground-parking scenes rendered with a full vehicle rig, an
**offline** reconstruction of the same data gives us an upper bound on what the
representation can express, and free-viewpoint top views rendered directly from
the Gaussian map already show the height information that IPM discards. The
incremental, streaming version does not yet reach that bound: closing the quality
gap between per-frame updates and full offline optimisation — by deciding *where*
a limited budget of new Gaussians should be spent, in particular near the seams
between adjacent cameras — is the open problem we are currently working on, along
with bringing the per-frame latency down to the camera frame rate.

<figure>
	<img src="/assets/images/projects/gs_topview_strip.jpg">
  <figcaption>Top view of the same scene, left to right: ground truth, inverse-perspective mapping, offline 3D Gaussian Splatting, and on-the-fly incremental 3D Gaussian Splatting. The offline column is the quality ceiling for the representation; the incremental column is the streaming result, and the difference between the two is what the current work targets.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, custom rasterizer kernels, fisheye and spherical camera
models, incremental pose estimation, COLMAP/SfM pipelines, Blender synthetic
data generation
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
