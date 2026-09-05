---
title: "Physics-Ready Assets and Digital Twins"
permalink: /Projects/physics-ready-twin/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/twin_teaser.jpg"
  image: "/assets/images/projects/twin_teaser.jpg"
---
A reconstructed scene is not yet a world. Photometric reconstruction — a
Gaussian-splat map, a mesh, a radiance field — tells you what a place *looks
like*, but a simulator needs to know what it is *made of*: which surfaces
belong to separate objects, where the collision boundaries lie, how heavy
things are, how much grip a surface offers. Everything downstream of
reconstruction in our stack — differentiable vehicle physics, residual policy
learning, closed-loop evaluation — depends on that missing half.

This project is about closing it: turning reconstructed scenes into
**physics-ready assets** that a physics engine can actually run, and into
**twins** whose behaviour can be checked against the real thing.

Our position on how to get there is deliberate: **we build on the open
reconstruction stack rather than reimplementing it.** Neural reconstruction
from real sensor data is now a solved-enough, well-supported problem, and the
research value for us sits in the step after it — binding physical semantics
to reconstructed geometry, and validating that the result behaves correctly
under contact.

Recent directions include:

1. **Reconstruction Backbone**: We adopt
   [NVIDIA Omniverse NuRec](https://developer.nvidia.com/omniverse/nurec) as
   the ingestion and reconstruction layer — a set of 3D Gaussian Splatting
   libraries that take real camera and lidar data and emit an OpenUSD scene
   that simulators can load. Its feed-forward variant,
   [Instant NuRec](https://github.com/NVIDIA/instant-nurec), replaces
   per-scene optimization with a single forward pass, which matters when the
   goal is to build many environments rather than one showcase scene.

2. **Object-level Decomposition**: Before mass, friction or articulation can
   be assigned to anything, the scene has to be separated into instances. We
   follow the scale-conditioned grouping line — 2D promptable masks lifted
   into a consistent 3D grouping over the Gaussian field, as implemented in
   [GARƒVDB](https://github.com/openvdb/fvdb-examples) — so that "this parked
   car", "this kerb", "this wall" become addressable entities rather than
   undifferentiated geometry.

3. **From Splats to Colliders**: A Gaussian field cannot be collided against;
   a surface can. We use the mesh-extraction path in
   [ƒVDB Reality Capture](https://github.com/openvdb/fvdb-reality-capture)
   — rendered stereo pairs, learned depth, truncated signed-distance fusion,
   sparse marching cubes — to obtain surfaces from which collision proxies can
   be derived.

4. **Explicit Collider Binding**: This is where our own engine work comes in.
   Visual geometry and collision geometry are kept as *separate, explicitly
   bound layers*: convex hulls, height fields and signed-distance volumes are
   attached to visual assets rather than derived from them at render time. The
   separation is what lets rendering fidelity and simulation stability be
   tuned independently — a collision proxy can be coarse and stable while the
   visual asset stays detailed. It also makes the binding inspectable, which
   matters more than it sounds: most contact bugs are visible immediately in a
   collider view and invisible in a rendered one.

<figure>
	<img src="/assets/images/projects/twin_collider_binding.jpg">
  <figcaption>Left: the collision layer alone — convex proxies, height fields and volumes bound to the scene's visual assets. Right: the same scene shaded, used as a physics test course with ramps, steps, drops and loose bodies to exercise contact behaviour.</figcaption>
</figure>

5. **Physical Property Estimation**: Geometry is only half of "physics-ready".
   Mass, inertia, friction and restitution have to be attached to each
   instance, and they cannot be read off a photograph. We estimate them by
   inversion instead — replaying observed motion in a differentiable simulator
   and back-propagating the discrepancy into the physical parameters, which is
   the same machinery described in our
   [Real2Sim & Sim2Real]({{ '/Projects/real2sim-sim2real/' | relative_url }})
   work.

6. **Validation by Driving**: A twin is only trustworthy to the extent that it
   has been driven. Each reconstructed environment is exercised on a test
   course — slopes, steps, drops, contact-rich clutter — and accepted only
   when a vehicle behaves in it the way it does in the physical world, which
   is also how we catch collider errors that no rendering metric reports.

**Where the open stack currently stops.** It is worth being precise about the
gap this project addresses. Reconstruction output is, in the general case,
*visual* geometry with no inherent collision properties; collision surfaces
are available only in specific depth-based workflows, and even there the
physical semantics — which mesh is a movable object, what it weighs, how it
grips — are still assigned by hand. Automating that assignment, and validating
it under contact, is the part we are taking on.

{% capture programming %}
#### programming experience
Python, PyTorch, CUDA, 3D Gaussian Splatting, OpenUSD, physics engines
(PhysX / Genesis), mesh processing and collision proxy generation, Isaac Sim
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
