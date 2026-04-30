---
layout: splash
permalink: /
hidden: true

header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/projects/p5_run_summary.png
  actions:
    - label: "<i class='fas fa-flask'></i> Our Research"
      url: "/docs/project/"
    - label: "<i class='fas fa-users'></i> Meet the Team"
      url: "/docs/people/"
  caption: "DIG Lab — Deep Imaging and Graphics"

excerpt: >
  Advancing the fundamentals of <i>Computer Graphics</i>, <i>Computer Vision</i>,
  and <i>Generative AI</i> — from real-time rendering engines to active digital
  twins, sim-to-real robot learning, and vision-language-action models.

feature_row:
  - image_path: /assets/images/projects/p1_vxgi_reflection.png
    alt: "Real-time Graphics Engine"
    title: "Real-time Graphics Engine"
    excerpt: "VXGI, DirectX 12 pipeline optimization, and advanced shadow rendering for production-quality real-time visuals."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/projects/p2_hair_dit.png
    alt: "Generative AI"
    title: "Generative AI for 3D Content"
    excerpt: "Diffusion-transformer architectures for controllable hair editing, neural dental texturing, and 3D-aware generation."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/projects/p5_alignment.png
    alt: "Active Digital Twin"
    title: "Active Digital Twin via 3DGS"
    excerpt: "On-the-fly 3D Gaussian Splatting with rig constraints, uncertainty-driven view planning, and medium reformulation."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"

feature_row2:
  - image_path: /assets/images/projects/p3_genesis_sim.png
    alt: "Genesis Sim2Real"
    title: "Genesis-based Sim-to-Real Transfer"
    excerpt: "Real-to-Sim calibration, residual reinforcement learning, and large-scale multi-agent training on the Genesis physics engine — bridging simulated policies to physical robots."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"

feature_row3:
  - image_path: /assets/images/wordcloud8.png
    alt: "AlphaMayo VLA"
    title: "AlphaMayo: Vision-Language-Action Models"
    excerpt: "A unified VLA foundation framework for language-conditioned manipulation, cross-embodiment generalization, and long-horizon planning — synergizing with our sim-to-real and active perception efforts."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"

feature_row4:
  - image_path: /assets/images/wordcloud7.png
    alt: "Open-Vocabulary Perception"
    title: "Open-Vocabulary Perception"
    excerpt: "Segmentation, detection, and instance discovery driven by foundation models — promptable concept segmentation, open-vocab 3D understanding, and video instance continuity."
    url: "/docs/project/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
---

We focus on
<br>1. <U>development of valuable imaging content incorporating the latest AI technology</U>, and
<br>2. <U>research on the underlying technology of AI-based imaging content</U>,
<br>based on the fundamentals of *<U>Computer Graphics</U>*, *<U>Computer Vision</U>*, and *<U>Generative AI</U>*.
<br><br>Our six active research thrusts span from low-level **graphics engine development** and **generative AI for 3D content**, to high-level **sim-to-real robot learning**, **vision-language-action models**, **active digital twins**, and **open-vocabulary perception**. Through industry–academic collaborations, we provide in-depth programming experiences ranging from native programming for experimental/commercial engine libraries to plug-in development for high-level editors such as Unreal Engine.

{% include feature_row %}

{% include feature_row id="feature_row2" type="left" %}

{% include feature_row id="feature_row3" type="right" %}

{% include feature_row id="feature_row4" type="left" %}
