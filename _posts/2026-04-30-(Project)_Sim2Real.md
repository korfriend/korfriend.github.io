---
title: "Real2Sim & Sim2Real — Genesis-based Physical Learning"
permalink: /Projects/real2sim-sim2real/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/p3_genesis_sim.png"
  image: "/assets/images/projects/p3_tank_rotate.png"
---
We develop a unified **Real2Sim / Sim2Real pipeline** built on the **Genesis**
physics engine, combining classical physics calibration, neural-physics
correction, and *residual learning* across both supervised and reinforcement
learning regimes. Our long-term goal is a closed-loop framework where (i)
real-world rollouts continuously calibrate the simulator, and (ii) policies
trained in the calibrated sim transfer back to the real platform with
quantifiable robustness.

Recent directions include:
1. **State-to-State (ST2ST) and Trajectory-to-State Mappers**: Lightweight
   neural mappers that align Genesis dynamics to observed real-world
   trajectories, reducing sim-to-real gap before policy learning starts.
2. **Residual Learning across Supervised + RL**: A behavior-cloned base
   policy is augmented by a *residual* reinforcement-learning head that
   compensates for covariate shift and unmodeled dynamics, achieving
   sub-millimeter trajectory drift on Genesis solver-optimized environments.
3. **Large-scale Multi-Agent Combat Simulation**: 3v3 tank-warfare
   environment with curriculum-based multi-agent reinforcement learning,
   scaling to thousands of parallel simulated worlds and credit-assignment
   designs that survive sparse rewards.
4. **Neural Physics**: Learned correction terms that augment classical
   simulators where calibration alone is insufficient (terrain, contact,
   suspension dynamics).

**Researchers**:
- [Dongwook Kang]({{ '/docs/people/' | relative_url }}) — ST2ST mapping and
  multi-agent RL combat simulation.
- [Jaewon Heo]({{ '/docs/people/' | relative_url }}) and
  [Mankyo Jung]({{ '/docs/people/' | relative_url }}) — trajectory-to-state
  mapping and RL-based path-following STB recovery.

<figure class="half">
	<img src="/assets/images/projects/p3_genesis_sim.png">
	<img src="/assets/images/projects/p3_tank_rotate.png">
  <figcaption>Genesis-based simulation environments (left) and multi-agent tank training (right).</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Genesis, Isaac Lab, Blender, RL frameworks (PPO/QMIX),
behavior cloning + residual RL pipelines
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
