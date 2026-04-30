---
title: "Vision-Language-Action Models for Robotics"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/wordcloud8.png"
  image: "/assets/images/wordcloud8.png"
---
We are developing the **AlphaMayo** framework, a Vision-Language-Action (VLA) foundation model for robot manipulation and embodied intelligence. Our research aims to bridge perception, language understanding, and motor control within a unified multimodal policy, enabling robots to follow natural-language instructions across diverse tasks and embodiments.

Recent directions include:
1. **Multimodal Policy Learning**: Joint training of vision encoders, language understanding modules, and action decoders for end-to-end manipulation policies that generalize across object categories and scene layouts.
2. **Cross-Embodiment Generalization**: Action representations and adapter strategies that transfer learned skills across heterogeneous robot platforms (industrial arms, mobile manipulators).
3. **Long-Horizon Task Planning**: Language-conditioned hierarchical planning that decomposes complex instructions into executable subgoals while respecting physical constraints and safety requirements.

This research synergizes with our Sim-to-Real (P3) and Active Digital Twin (P5) efforts — simulation pretraining feeds VLA models, while active perception sharpens grounding for real-world deployment.

{% capture programming %}
#### programming experience
Python, PyTorch, Hugging Face Transformers, robotics middleware (ROS2), simulation (Genesis, Isaac Lab)
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
