---
title: "Real2Sim & Sim2Real — Differentiable Vehicle Physics and Control"
permalink: /Projects/real2sim-sim2real/
date: 2026-04-30 -0000
categories:
  - Projects
header:
  teaser: "/assets/images/projects/phys_world_teaser.jpg"
  image: "/assets/images/projects/phys_world_teaser.jpg"
---
We build an **explicit, state-space world model** for vehicles — an executable
world in which geometry, contacts and material parameters are represented
explicitly, and on top of which a car can be identified, controlled and
trained. Unlike pixel-level or latent world models that predict future frames,
every quantity here is a real state variable: pose, velocity, wheel contact,
mass, friction. The simulation is therefore causal, reproducible, and open to
gradient-based identification, and rendering becomes a *consequence* of that
state rather than the model itself.

The physics layer is built on the **Genesis** engine — GPU-batched parallel
environments, deterministic state transitions, runtime domain randomization,
and, most importantly, a **differentiable dynamics kernel**. Because gradients
flow through the whole simulator, real-world driving error can be
back-propagated into physical parameters (Real2Sim system identification), and
the control that produces a target trajectory can be solved directly instead of
being searched for by trial and error.

Recent directions include:

1. **Hybrid Control — Offline Inverse Look-up with Feedback**: Differentiable
   inverse control is accurate but costs about 299 ms per control step. We
   instead sweep the drive-train offline into a (speed × throttle →
   acceleration) table, invert that table at run time, and close the loop with
   a PD steering correction. This runs in 0.056 ms per step — roughly 5,300×
   faster — while tracking at least as well (0.044 m mean cross-track error
   against 0.078 m), leaving the differentiable solver for offline
   identification where its cost is affordable.

2. **Differentiable Physics Where the Table Stops Working**: A look-up table
   only covers the states it was swept over, and its size grows
   combinatorially with state dimension — from 78K entries in four dimensions
   to 42M once steering angle, lateral velocity and yaw rate are added. When
   the vehicle leaves the tabulated regime — halving its mass mid-run, for
   instance — the table-driven controller deviates by 3.9 m, while the
   differentiable controller, which re-solves the control at every step, stays
   within 0.3 m. Nominal driving therefore runs on the fast table; off-nominal
   conditions fall back to differentiable re-solving.

<figure>
	<img src="/assets/images/projects/phys_sweep_vs_diff.jpg">
  <figcaption>Differentiable inverse control (left) against the offline sweep table with run-time inverse look-up (right), without (top) and with (bottom) PD feedback. Numbers are mean / maximum cross-track and speed error. The table is ~5,300× cheaper per step at comparable accuracy.</figcaption>
</figure>

<figure class="half">
	<img src="/assets/images/projects/phys_offnominal.jpg">
  <figcaption>Off-nominal robustness: with the vehicle mass halved mid-run — a state the sweep table never covered — the tabulated controller leaves the path (3.9 m maximum deviation) while the differentiable controller re-solves each step and holds it (0.3 m).</figcaption>
</figure>

3. **A Four-Stage Control Stack**: Physics-consistent trajectory generation
   feeds a nominal tracking controller (behavior-cloned steering with
   PID/feed-forward speed control), which is corrected by a residual
   reinforcement-learning head and finally constrained by a deterministic
   safety shield. The residual is deliberately *gated* — scaled by a risk
   estimate and by lateral acceleration — so it stays inert while the nominal
   controller is performing well, and intervenes only in out-of-distribution
   regimes. It corrects steering and applies braking; throttle is left to the
   nominal controller, which already tracks speed to 0.049 m/s.

<figure>
	<img src="/assets/images/projects/phys_control_stack.jpg">
  <figcaption>The four-stage stack: physics-consistent path generation, nominal tracking, gated residual correction, and a deterministic safety shield.</figcaption>
</figure>

4. **Safety as Structure, Not as Reward**: Across 660 safety-critical crossing
   scenarios, a residual RL policy alone tracks well (0.061 m) but fails 58.5%
   of the time; a rule-only shield is far safer but destroys tracking (5.96 m,
   10.0% failure). Composing them — a learned residual constrained by a
   deterministic STOP/PASS shield — gives 1.5% failure at 0.090 m tracking
   error, and the remaining failures are all physically unavoidable. Collision
   penalties in the reward were not sufficient to induce sustained yielding;
   the constraint has to be imposed structurally rather than learned.

<figure>
	<img src="/assets/images/projects/phys_safety_4arm.jpg">
  <figcaption>Ablation over the same crossing scenario. Learning supplies tracking and the rule supplies safety: neither alone is sufficient, and only their composition (B′) both follows the path and yields.</figcaption>
</figure>

5. **Off-Nominal Recovery by Planning**: When a disturbance — a spin, a lateral
   impact, an adverse spawn pose — throws the vehicle off its reference path,
   we generate a feasible recovery path rather than learning a recovery policy.
   Frenet-quintic and Dubins candidates are filtered by steering-limit and
   braking-distance feasibility, ranked by path length, merge distance,
   curvature load, steering effort and speed loss, and merged back into the
   original path. Compared with a learned recovery policy this leaves the
   nominal stack untouched, remains inspectable when it fails, and is corrected
   by editing rules instead of retraining.

6. **Terrain Diversity for Generalization**: Training the residual policy over
   99 paths spread across multiple 3 km × 3 km terrains transfers to unseen
   environments better than long-horizon training on a single 500 m terrain
   (8.89 cm against 10.41 cm cross-track error on the held-out environment),
   and reaches it in roughly a third of the wall-clock time. Environment
   diversity, not episode length, is what buys generalization here.

7. **Planner Integration (in progress)**: We are connecting a
   vision-language-action planner as the trajectory proposer, with our nominal
   controller executing the proposed trajectory and the safety shield
   constraining it — the planner proposes, the controller tracks, and the
   shield enforces what must hold.

<figure>
	<video autoplay loop muted playsinline style="width:100%;">
		<source src="/assets/images/projects/sim2sim.mp4" type="video/mp4">
		Your browser does not support the video tag.
	</video>
  <figcaption>Sim2Sim calibration: an observed trajectory is converted into the steering and throttle commands that reproduce it under a different physics engine, which is the same mechanism used to align the simulator to real-world rollouts.</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, PyTorch, Genesis, differentiable simulation, Isaac Lab, Blender,
RL frameworks (PPO/QMIX), behavior cloning + residual RL, trajectory planning
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
