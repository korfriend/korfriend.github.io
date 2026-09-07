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
	<div style="flex:0 0 100%;width:100%;display:grid;grid-template-columns:1fr 1fr;gap:1.2em 1.3em;margin-bottom:.7em;">
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">Inverse-perspective mapping</div>
			<video src="/assets/images/ipm_reproj.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Top view of a parking manoeuvre produced by re-projecting the fisheye images onto the ground plane; neighbouring vehicles are smeared flat along the viewing direction."></video>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">3D Gaussian Splatting reconstruction</div>
			<video src="/assets/images/gs_svm.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="The same manoeuvre rendered from the reconstructed Gaussian map, where the neighbouring vehicles keep their height and outline."></video>
		</div>
	</div>
  <figcaption>The same parking manoeuvre under inverse-perspective mapping (left) and 3D Gaussian Splatting reconstruction (right). Planar re-projection collapses the neighbouring vehicles into smears on the ground and holds a single fixed viewpoint; the reconstructed map preserves their height and outline and can be rendered from anywhere.</figcaption>
</figure>

An explicit 3D map removes that assumption. The question we work on is **how
good such a map can be made while it is still being built during the drive**,
from a camera rig that is wide-angle, low-overlap and rigidly fixed to a moving
body.

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

On synthetic underground-parking sequences rendered from a full vehicle rig, the
pipeline already runs at **interactive time**: the map is updated as frames
arrive and can be rendered from a free viewpoint while the manoeuvre is still in
progress, and those free-viewpoint top views already carry the height
information that IPM discards. An **offline** reconstruction of the same data
serves as the ceiling — what these Gaussians can express when the whole sequence
is optimised at once, with no per-frame budget at all.

**Raising quality at interactive time is the current work.** We treat the update
rate as a fixed constraint rather than something to trade away: the question is
how much of the offline quality can be recovered while the map keeps updating
during the drive. In practice that comes down to two decisions made every frame
— where a limited budget of new Gaussians should be spent, and how much of the
existing map can be corrected before the update stops keeping pace with the
cameras. The streaming result thins out first at the seams between adjacent
fisheye views and on surfaces that only become visible late in the manoeuvre,
which is where that budget currently goes.

<figure>
	<video src="/assets/images/svm_comparison.mp4" autoplay loop muted playsinline preload="metadata" style="flex:0 0 100%;width:100%;display:block;" aria-label="Four synchronized top views of the same parking manoeuvre: ground truth, inverse-perspective mapping, offline 3D Gaussian Splatting, and on-the-fly incremental 3D Gaussian Splatting."></video>
  <figcaption>Top view of the same manoeuvre, left to right: ground truth, inverse-perspective mapping, offline 3D Gaussian Splatting, and on-the-fly incremental 3D Gaussian Splatting. The offline column is the quality ceiling for the representation; the incremental column is what the map looks like while it is still being built, and the distance between the two is what the current work is closing.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, custom rasterizer kernels, fisheye and spherical camera
models, incremental pose estimation, COLMAP/SfM pipelines, Blender synthetic
data generation
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
