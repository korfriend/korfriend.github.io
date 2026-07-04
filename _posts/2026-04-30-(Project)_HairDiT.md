---
title: "Conditioned DiT for Sketch Hair Editing"
permalink: /Projects/hair-style-dit/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/hair_conditioned_dit_teaser.jpg"
  image: "/assets/images/projects/hair_conditioned_dit_teaser.jpg"
---
We study **sketch-based hair editing on a frozen diffusion-transformer (DiT)
backbone**. Building on our prior GAN-inversion work for hairstyle
manipulation, we attach a lightweight sketch **ControlNet** to a frozen DiT
generative prior and ask a focused question: *when the sketch is used to edit
hair, what does the hair matte add?* The goal is portrait hair that is at once
faithful to the user's colored strokes and naturally embedded in the face.

Recent directions include:
1. **Matte-Conditioned Sketch Latents**: We build the condition on the frozen
   VAE latent of the *colored* sketch — so hair tone is controlled directly by
   the strokes — and add two complementary matte signals on the ControlNet: a
   learnable, region-aware bias that steers the latent *inside* the hair
   region, and a concatenated raw matte that anchors the edit region. Their
   gains are additive.
2. **Optional Residual Gating — a Hairstyle-Dependent Trade-off**: A training
   choice that makes loose hair more seamless and more faithful to the sketch,
   while braided styles read better without it — a controllable qualitative
   knob rather than a one-size-fits-all setting.
3. **Leakage-Free Evaluation**: We expose an evaluation pitfall — under the
   standard ground-truth-background protocol, the frozen DiT's global attention
   lets the preserved background *leak* hair cues into the generated
   foreground, flattering sketch-only conditioning and hiding the value of the
   matte. A leakage-free, novel-color, cross-identity protocol removes this
   artifact and reveals that matte conditioning makes the generated hair
   markedly more realistic.
4. **Training-Free Portrait Preservation**: The surrounding portrait is kept
   intact through a training-free latent blending step, so edits stay confined
   to the hair while identity, skin, and background are preserved.

<figure>
	<img src="/assets/images/projects/hair_comparison_grid.jpg">
  <figcaption>Qualitative comparison of sketch-based hair editing. Given a source portrait and a matte+sketch input, our matte-conditioned frozen-DiT approach produces hair that follows the strokes while staying realistic and naturally embedded in the portrait, compared against representative sketch-, reference-, and text-driven baselines.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Diffusers, frozen DiT backbones + ControlNet conditioning, VAE latent manipulation, training-free latent blending, hair matte estimation
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
