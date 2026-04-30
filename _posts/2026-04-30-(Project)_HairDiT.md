---
title: "DiT-based Controllable Hair Style Editing"
permalink: /Projects/hair-style-dit/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/hairtransfer.jpg"
  image: "/assets/images/hairtransfer.jpg"
---
We build **controllable hair-editing systems** on top of diffusion-transformer
(DiT) backbones. Building on our prior GAN-inversion work for hairstyle
manipulation, this line of research moves to modern DiT generative priors
and explores precise, sketch-driven, identity-preserving hair editing for
realistic portrait imagery.

Recent directions include:
1. **Sketch-guided Hair Inpainting**: User-provided strokes condition the
   generation of new hairstyles that respect both the input sketch and the
   surrounding facial context.
2. **Matte-gated ControlNet**: A novel control architecture that uses
   per-pixel hair mattes to gate residual conditioning, enabling
   high-fidelity editing without leaking content into non-hair regions.
3. **Context-robust DiT Generation**: Studying how DiT generators interact
   with surrounding context (face geometry, illumination), and proposing
   conditioning strategies that yield robust generations across diverse
   inputs.

<figure>
	<img src="/assets/images/hairtransfer.jpg">
  <figcaption>Hair editing — bridging earlier GAN-inversion work with our DiT-based pipeline.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Diffusers, ControlNet/DiT frameworks
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
