---
title: "GAN-Inversion with StyleGAN2"
date: 2021-06-01 -0000
categories:
  - Projects
#tags:
#  - StyleGAN2
#  - GAN-inversion
#  - Hair Editing

header:
  teaser: "/assets/images/deep_gm_teasor.jpg"
  image: "/assets/images/hairtransfer.jpg"
---
We have explored **GAN-inversion with StyleGAN2** as a powerful tool for
high-fidelity hairstyle manipulation. Building on the latent-space structure
of StyleGAN2, our research focused on improving semantic alignment between
source and reference images and on producing detailed, artifact-free hair
transfer results.

The core technical contributions of this line of work include:

1. **Structural Integration with Refined Mask Completion** — improving
   semantic alignment between the source image and the reference style,
   which substantially reduces blending artifacts during hair transfer.
2. **Improved Latent Code Optimization** — combining masked perceptual
   and style components in the inversion objective so that fine-grained
   hair attributes such as color fidelity and strand-level texture are
   preserved.
3. **Reference- and Sketch-Based Editing** — supporting both
   reference-image-driven and sketch-driven hair editing through a
   unified inversion pipeline, packaged with a Streamlit-based interactive
   web interface.

This work — released as
[**VividHair**](https://github.com/agliotomato/VividHair) —
demonstrates clear improvements over prior state-of-the-art hair
manipulation techniques in both generation quality and usability.
The insights from StyleGAN2 inversion directly inform our current
**DiT-based hair-editing program**, where we move from GAN-inversion to
diffusion-transformer priors for the next generation of controllable
generation.

<figure>
	<img src="/assets/images/hairtransfer.jpg">
  <figcaption>Hair transfer results from StyleGAN2-based GAN inversion.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, StyleGAN2, encoder4editing, Streamlit
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
