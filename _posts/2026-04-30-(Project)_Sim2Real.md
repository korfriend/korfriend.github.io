---
title: "Genesis-based Sim-to-Real Transfer"
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p3_genesis_sim.png"
  image: "/assets/images/projects/p3_tank_rotate.png"
---
We develop sim-to-real transfer frameworks that bridge simulated training environments and physical systems using the Genesis physics engine. Our approach combines physics-informed Real-to-Sim calibration with hybrid imitation and reinforcement learning, enabling efficient policy learning in calibrated simulations that transfer robustly to real-world deployment.

Recent directions include:
1. **Real-to-Sim Calibration**: State-level and trajectory-level mappers that tune Genesis parameters from real-world vehicle dynamics to align simulated trajectories with physical observations.
2. **Residual Reinforcement Learning**: A hybrid Behavior Cloning + Residual RL approach for path-following control, achieving sub-millimeter trajectory drift on Genesis solver-optimized environments.
3. **Multi-Agent Combat Simulation**: A 3v3 tank warfare environment with curriculum-based multi-agent reinforcement learning, scaling to thousands of parallel simulated worlds.

<figure class="half">
	<img src="/assets/images/projects/p3_genesis_sim.png">
	<img src="/assets/images/projects/p3_tank_rotate.png">
  <figcaption>Genesis-based simulation environments (left) and multi-agent tank training (right).</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Genesis, Isaac Lab, Blender, RL frameworks (PPO/QMIX)
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
