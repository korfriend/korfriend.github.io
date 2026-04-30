---
title: "Domain-Optimized Segmentation via SAM3 Attention Tuning"
permalink: /Projects/domain-segmentation/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/wordcloud7.png"
  image: "/assets/images/wordcloud7.png"
---
We investigate **domain-optimized segmentation** by tuning the **attention
mechanisms inside SAM 3-class foundation models** so that promptable
concept segmentation can be specialized to demanding downstream domains
without losing the open-vocabulary flexibility of the backbone. The aim
is a small, principled modification surface — restricted to attention
adapters and prompt encoders — that leaves the foundation weights mostly
intact while adapting to fine-grained, domain-specific concepts.

Recent directions include:
1. **Attention-Mechanism Tuning of SAM3**: Surgical adapters into the
   self/cross-attention layers of SAM3, conditioned by domain-specific
   prompt encoders, to specialize the segmenter without full fine-tuning.
2. **Tooth-Number-Aware Dental Segmentation** (planned): Per-tooth
   identity segmentation for intra-oral imaging, supplying the labels
   our dental inverse-graphics pipeline needs for crown-level analysis.
3. **Hair-Structure Segmentation** (planned): Strand-aware hair masking
   that downstream feeds the matte-gated DiT hair-editing pipeline,
   coupling perception and generation in a single workflow.

This research line provides instance-level priors that feed back into our
**Dental Inverse Graphics** and **Hair DiT** projects, closing a loop
between perception and generation.

{% capture programming %}
#### programming experience
Python, PyTorch, Hugging Face Transformers, SAM/SAM2/SAM3 frameworks, OpenCV
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
