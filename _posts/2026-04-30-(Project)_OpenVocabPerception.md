---
title: "Open-Vocabulary Perception: Segmentation, Detection, Instancing"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/wordcloud7.png"
  image: "/assets/images/wordcloud7.png"
---
We investigate open-vocabulary perception techniques for segmentation, detection, and instance discovery in 2D and 3D scenes. Our research builds on recent foundation models such as **Promptable Concept Segmentation (PCS)** and SAM-family architectures to enable flexible, language-driven scene understanding for downstream robotics and digital-twin applications.

Recent directions include:
1. **Promptable Concept Segmentation**: Text/click-promptable segmentation pipelines for arbitrary object concepts, including rare and compositional categories beyond closed-set vocabularies.
2. **Open-Vocabulary 3D Perception**: Lifting 2D foundation-model features into 3D scenes for instance-level understanding of NeRF/3DGS reconstructions, enabling object-centric editing and manipulation.
3. **Video Instance Continuity**: Temporal consistency mechanisms for instance identity tracking across long video sequences, supporting robust scene understanding for active perception.

This work feeds the **VLA (P4)** project with grounded object references for language-conditioned manipulation, and provides instance-level priors for the **Active Digital Twin (P5)** next-best-view planner.

{% capture programming %}
#### programming experience
Python, PyTorch, Hugging Face Transformers, SAM/SAM2 frameworks, OpenCV
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
