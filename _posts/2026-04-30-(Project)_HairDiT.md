---
title: "Sketch-based Hair Editing with Generative Priors"
permalink: /Projects/hair-style-dit/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/hair_demo_ui.jpg"
  image: "/assets/images/projects/hair_demo_ui.jpg"
---
We work on **sketch-driven hair editing for portrait images**. The user draws
coloured strokes over a photograph — indicating where hair should go, how it
should flow, and what colour it should take — and the system regenerates the
hair accordingly while leaving identity, skin and background untouched.
Building on our earlier GAN-inversion work for hairstyle manipulation, the
current line of work attaches lightweight conditioning to a frozen
diffusion-transformer prior, so that the strong appearance prior of a
large pretrained generator can be steered by a sparse, hand-drawn signal.

The interactive tool below is the working front end for this research: a face
image, a hair region and a set of colour strokes go in, and an edited portrait
comes out.

<figure>
	<img src="/assets/images/projects/hair_demo_ui.jpg">
  <figcaption>Interactive sketch-based hair editing: the user paints the hair region and draws coloured strokes on the left, and the edited portrait is generated on the right.</figcaption>
</figure>

**Publication status.** A conference paper covering this work was recently
submitted and is currently under review. Method details, quantitative results
and code will be posted here once the review process concludes.

{% capture programming %}
#### programming experience
Python, PyTorch, Diffusers, diffusion-transformer backbones, conditional
generation, VAE latent manipulation, interactive web demo
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
