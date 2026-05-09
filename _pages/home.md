---
layout: splash
permalink: /
hidden: true

header:
  overlay_color: "#000"
  overlay_filter: "0.6"
  overlay_image: /assets/images/projects/p5_run_summary.png
  actions:
    - label: "<i class='fas fa-flask'></i> Research Projects"
      url: "/docs/project/"
    - label: "<i class='fas fa-users'></i> Meet the Team"
      url: "/docs/people/"
  caption: "DIG Lab — Deep Imaging and Graphics"

tagline: >
  **&ldquo;AI is the pitch. Not the finish line.&rdquo;**<br><br>
  AI is about getting ideas out of your head &mdash; leveraging your potential, for people to see the vision.<br><br>
  **AI is your insight transformer.**
---

## Who We Are

The **Deep Imaging and Graphics (DIG) Lab** pursues research at the
intersection of **computer graphics, computer vision, and generative AI**.
We believe the most exciting problems sit *between* these fields — where
physically-grounded rendering meets learned generative priors, and where
simulation, reconstruction, and perception become parts of a single imaging
stack.

## What We Aim For

- **End-to-end imaging stack.** From low-level GPU rendering pipelines to
  high-level learned perception and generation, we build technology along
  the entire imaging stack — and care that every layer is implementable,
  measurable, and robust.
- **Bridging classical and learned models.** We treat *physically-based
  rendering*, *neural representations* (3DGS, NeRF), and *generative
  diffusion models* as complementary tools, and develop principled
  combinations such as inverse graphics with DiT priors, or medium-aware
  3DGS with differentiable rendering.
- **Real systems, real impact.** Our research is grounded in real
  applications — dental imaging, hairstyle editing, multi-camera digital
  twins, robotic sim-to-real — and feeds back into a shared in-house
  graphics engine that the whole lab uses.

## Where We Came From, Where We're Going

Over the past decade, the lab has built and shipped an **in-house graphics
engine** used in commercial medical visualization solutions, applied
graphics-based techniques to **traditional sensor imaging** and to
**non-destructive inspection / medical examination** systems, and
contributed to **AR navigation** for surgical workflows. Building on this
foundation in classical computer graphics and computer vision, we have
also leveraged high-end content engines such as **Blender** and **Unreal
Engine** to author **immersive applications** and to build
**verification-oriented simulation** environments.

Our current research carries that same DNA — *deep engineering combined
with learning* — into:

- **Modern in-house graphics engines** (DX12, VXGI, advanced shadows)
- **Dental realistic inverse graphics** (DiT + 3D Gaussian Splatting)
- **DiT-based controllable hair editing**
- **3D Gaussian Splatting** — medium-aware models and high-speed
  on-the-fly reconstruction
- **Real2Sim / Sim2Real** with the **Genesis** physics engine —
  inverse-dynamics and trajectory-to-controls (ST, B) mappers, residual
  RL, large-scale multi-agent simulation
- **Domain-optimized segmentation** via SAM 3-class attention tuning

See the [Research Projects]({{ '/docs/project/' | relative_url }}) page for
details on each line, including the students and concrete results.

## Looking for Students Ready to Push the Boundary

We are actively looking for **motivated undergraduate, master's, and Ph.D.
students** who want to do hands-on research that combines deep engineering
with modern AI:

- You like building real systems — engines, simulators, training pipelines —
  not only writing papers about them.
- You want to work *across* graphics, vision, and generative AI, instead of
  staying inside a single sub-area.
- You enjoy reading the literature *and* getting your hands dirty across the
  full graphics–AI stack — from **native graphics APIs and engine-level
  code** (Vulkan, DX12, CUDA) and **modern ML frameworks** (PyTorch,
  TensorFlow), through **differentiable rendering and physics simulators**
  (Mitsuba, Genesis), all the way up to **high-level editors and toolkits**
  (Unreal Engine, Three.js).

If that sounds like you, please reach out — we have open projects across all
six research lines above, and we welcome new students who are ready for a
challenge.

<small>
Contact: <a href="mailto:korfriend@gmail.com">korfriend@gmail.com</a> &nbsp;|&nbsp;
[More about the lab head]({{ '/docs/people/' | relative_url }})
</small>
