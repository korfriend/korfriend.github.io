---
title: "Real2Sim & Sim2Real — Aligning Dynamics Across Physics Systems"
permalink: /Projects/real2sim-sim2real/
date: 2026-04-30 -0000
published: true
categories:
  - Projects
header:
  teaser: "/assets/images/projects/phys_sim_world_teaser.jpg"
  image: "/assets/images/projects/phys_sim_world_teaser.jpg"
---
Two physics systems never agree. Record a vehicle following a path — in the
real world, or in another simulator — then feed exactly the same steering and
throttle into a different engine, and the vehicle will not follow the same
path. Tire model, contact solver, integrator, mass distribution: every one of
them differs, and the errors compound.

That disagreement is the core problem of this project. **We work on aligning
dynamics across different physics systems** — recovering, for a target physics
engine, the control inputs that make it reproduce an observed trajectory. This
is what makes a simulator a usable stand-in for the real world, and it is the
foundation everything else here is built on: without it, a policy trained in
simulation is trained against the wrong physics.

## Path2ST — converting a path into the target system's controls

Our approach does not replay controls; it re-derives them. A reference
trajectory is expressed in system-independent kinematic terms — curvature and
acceleration along the path — and then converted into the steering and throttle
that the *target* dynamic system needs in order to realize it. We call this
**Path2ST**.

<figure>
	<video src="/assets/images/blender_genesis_st.mp4" autoplay loop muted playsinline preload="metadata" style="flex:0 0 100%;width:100%;display:block;" aria-label="Three synchronized top-down views: a reference run in Blender, the same controls replayed open-loop in Genesis drifting off the reference, and the Path2ST-converted controls tracking it."></video>
  <figcaption>Cross-system transfer. A trajectory recorded in the source system (left, Blender) is reproduced in the target engine two ways. Replaying the source steering and throttle open-loop (middle) drifts steadily away from the reference — the two engines do not share a dynamics model, so identical inputs do not produce identical motion. Converting the path through Path2ST into controls appropriate to the target dynamics (right) keeps the vehicle on the reference throughout the manoeuvre.</figcaption>
</figure>

<figure>
	<video src="/assets/images/blender_genesis_st2.mp4" autoplay loop muted playsinline preload="metadata" style="flex:0 0 100%;width:100%;display:block;" aria-label="A reference path with curvature and acceleration readouts on the left, mapped through Path2ST to steering and throttle values driving the target vehicle on the right."></video>
  <figcaption>The conversion itself, running along the path: curvature and longitudinal acceleration sampled at each point of the reference (left) are mapped to the steering and throttle the target vehicle model requires at that instant (right).</figcaption>
</figure>

## How the conversion is made fast and precise

The conversion has to run inside the control loop, which rules out solving it
the expensive way. Differentiable inverse control — back-propagating through
the simulator to find the control that produces the desired next state — is
accurate but costs about **299 ms per step**.

Instead we sweep the vehicle's drive-train offline into a lookup table over
speed and throttle against acceleration, invert that table at run time, and
close the loop with a **PD steering correction**. Building the table takes 14
seconds, once. Control then costs **0.056 ms per step — roughly 5,300× less** —
and tracks at least as well: 0.044 m mean cross-track error against 0.078 m,
with a maximum of 0.100 m. **High-speed, precise control is what this
combination buys**, and it is what makes the aligned simulator usable in a
closed loop rather than only offline.

<figure>
	<div style="flex:0 0 100%;width:100%;display:grid;grid-template-columns:1fr 1fr;gap:1.2em 1.3em;margin-bottom:.7em;">
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">Differentiable inverse control · feed-forward only</div>
			<video src="/assets/images/diff_only.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Differentiable inverse control tracking the reference path without PD feedback."></video>
			<div style="font-size:.75em;opacity:.72;margin-top:.3em;">cross-track 0.402 / 0.833 m &middot; speed 0.682 / 1.744 m/s</div>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">Sweep table + inverse look-up · feed-forward only</div>
			<video src="/assets/images/table_only.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Sweep-table inverse look-up tracking the reference path without PD feedback."></video>
			<div style="font-size:.75em;opacity:.72;margin-top:.3em;">cross-track 0.623 / 2.780 m &middot; speed 0.592 / 1.127 m/s</div>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">Differentiable inverse control · with PD feedback</div>
			<video src="/assets/images/diff_pd.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Differentiable inverse control tracking the reference path with PD feedback."></video>
			<div style="font-size:.75em;opacity:.72;margin-top:.3em;">cross-track 0.044 / 0.100 m &middot; speed 0.711 / 1.908 m/s</div>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">Sweep table + inverse look-up · with PD feedback</div>
			<video src="/assets/images/table_pd.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Sweep-table inverse look-up tracking the reference path with PD feedback."></video>
			<div style="font-size:.75em;opacity:.72;margin-top:.3em;">cross-track 0.078 / 0.244 m &middot; speed 0.186 / 1.124 m/s</div>
		</div>
	</div>
  <figcaption>Differentiable inverse control (left) against the offline sweep table with run-time inverse look-up (right), without (top) and with (bottom) PD feedback. Figures under each panel are mean / maximum cross-track and speed error over the run.</figcaption>
</figure>

**Differentiable physics is kept for where precise simulation is actually
required** — offline system identification, and states the table never covered.
A lookup table only spans the region it was swept over, and grows
combinatorially with state dimension: 78K entries in four dimensions, 42M once
steering angle, lateral velocity and yaw rate are added. Halve the vehicle's
mass mid-run and the tabulated controller leaves the path by 3.9 m, while the
differentiable controller — re-solving the control at every step — holds it
within 0.3 m. The two are complements rather than competitors: the table
drives, and the differentiable solver identifies and rescues.

## Building a control system inside the aligned world

Once the simulator's dynamics are aligned to the target system, it becomes a
place where a full control stack can be developed and evaluated rather than
merely animated. That stack is the second half of this project:

1. **Physics-consistent path generation** — reference trajectories the vehicle
   model can actually execute, with their optimal control pairs extracted
   through the sweep table and PD controller.
2. **Nominal tracking (Path2ST)** — behavior-cloned steering with PID and
   feed-forward speed control, following the reference in real time.
3. **Residual reinforcement learning** — a gated correction that stays inert
   while the nominal controller performs well, and compensates steering error
   only in out-of-distribution regimes such as hard braking or sharp turns.
4. **Deterministic safety shield** — a STOP/PASS constraint imposed on the
   policy's output when a crossing conflict is predicted.

<figure>
	<div style="flex:0 0 100%;width:100%;display:grid;grid-template-columns:1fr 1fr;gap:1.2em 1.3em;margin-bottom:.7em;">
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">&#9312; SimPath &middot; path generation</div>
			<video src="/assets/images/simpath.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Generation of a physics-consistent reference path."></video>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">&#9313; Path2ST &middot; nominal tracking</div>
			<video src="/assets/images/path2st.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Nominal controller tracking the reference path in real time."></video>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">&#9314; Residual RL &middot; error compensation</div>
			<video src="/assets/images/path2st_rl.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Gated residual reinforcement-learning correction on top of the nominal controller."></video>
		</div>
		<div>
			<div style="font-weight:700;font-size:.82em;margin-bottom:.32em;">&#9315; Safety shield &middot; STOP / PASS</div>
			<video src="/assets/images/safty_shield_ov.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Deterministic safety shield overriding the policy with a STOP or PASS decision at a crossing conflict."></video>
		</div>
	</div>
  <figcaption>The four-stage stack: physics-consistent path generation, nominal tracking, gated residual correction, and a deterministic safety shield.</figcaption>
</figure>

The division of labour between the learned and the imposed parts is deliberate,
and measurable. Across 660 safety-critical crossing scenarios, a residual
policy alone tracks well (0.061 m) but fails 58.5% of the time; a rule-only
shield is safe but destroys tracking (5.96 m, 10.0% failure). Composed, they
give 1.5% failure at 0.090 m tracking error, and the remaining failures are
physically unavoidable. Collision penalties in the reward were not sufficient
to induce sustained yielding — the constraint has to be structural rather than
learned.

<figure>
	<div style="flex:0 0 100%;width:100%;display:grid;grid-template-columns:1fr 1fr;gap:1.2em 1.3em;margin-bottom:.7em;">
		<div>
			<div style="position:relative;line-height:0;">
				<video src="/assets/images/safety_shield_RL.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Residual RL alone at the crossing conflict, ending in a collision."></video>
				<span style="position:absolute;top:8px;right:8px;background:rgba(15,22,36,.8);color:#fff;font:700 .74em/1.35 inherit;padding:3px 8px;border-radius:3px;">A &middot; RL only</span>
				<span style="position:absolute;left:8px;bottom:8px;background:#c0392b;color:#fff;font:700 .74em/1.35 inherit;letter-spacing:.04em;padding:3px 9px;border-radius:3px;">COLLISION</span>
			</div>
			<div style="font-size:.75em;opacity:.72;margin-top:.32em;">cross-track 0.061 m &middot; failure 58.5 % (386 / 660)</div>
		</div>
		<div>
			<div style="position:relative;line-height:0;">
				<video src="/assets/images/safety_shield_RL_rule.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="Residual RL under the deterministic safety shield, yielding and then passing without collision."></video>
				<span style="position:absolute;top:8px;right:8px;background:rgba(15,22,36,.8);color:#fff;font:700 .74em/1.35 inherit;padding:3px 8px;border-radius:3px;">B&prime; &middot; RL + Rule</span>
				<span style="position:absolute;left:8px;bottom:8px;background:#1e8449;color:#fff;font:700 .74em/1.35 inherit;letter-spacing:.04em;padding:3px 9px;border-radius:3px;">SAFE</span>
			</div>
			<div style="font-size:.75em;opacity:.72;margin-top:.32em;">cross-track 0.090 m &middot; failure 1.5 % (10 / 660)</div>
		</div>
		<div>
			<div style="position:relative;line-height:0;">
				<video src="/assets/images/safety_shield_rule.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="The rule-only shield without a learned residual, losing the path and colliding."></video>
				<span style="position:absolute;top:8px;right:8px;background:rgba(15,22,36,.8);color:#fff;font:700 .74em/1.35 inherit;padding:3px 8px;border-radius:3px;">C &middot; Rule only</span>
				<span style="position:absolute;left:8px;bottom:8px;background:#c0392b;color:#fff;font:700 .74em/1.35 inherit;letter-spacing:.04em;padding:3px 9px;border-radius:3px;">COLLISION</span>
			</div>
			<div style="font-size:.75em;opacity:.72;margin-top:.32em;">cross-track 5.961 m &middot; failure 10.0 % (66 / 660)</div>
		</div>
		<div>
			<div style="position:relative;line-height:0;">
				<video src="/assets/images/safety_shield_baseline.mp4" autoplay loop muted playsinline preload="metadata" style="width:100%;display:block;" aria-label="The nominal controller alone with neither residual nor shield, colliding at the crossing."></video>
				<span style="position:absolute;top:8px;right:8px;background:rgba(15,22,36,.8);color:#fff;font:700 .74em/1.35 inherit;padding:3px 8px;border-radius:3px;">D &middot; Baseline only</span>
				<span style="position:absolute;left:8px;bottom:8px;background:#c0392b;color:#fff;font:700 .74em/1.35 inherit;letter-spacing:.04em;padding:3px 9px;border-radius:3px;">COLLISION</span>
			</div>
			<div style="font-size:.75em;opacity:.72;margin-top:.32em;">cross-track 4.546 m &middot; failure 83.5 % (551 / 660)</div>
		</div>
	</div>
  <figcaption>Ablation over the same crossing scenario &mdash; same scene, same camera, same playback speed. Learning supplies tracking and the rule supplies safety; only their composition (B&prime;) achieves both. Figures under each panel are mean cross-track error and failure rate over 660 safety-critical scenarios.</figcaption>
</figure>

Two further results shape how the stack is trained and recovered. Off-nominal
recovery is handled by **planning rather than by a learned policy** —
Frenet-quintic and Dubins candidates filtered by steering and braking
feasibility, ranked by path length, merge distance, steering effort and speed
loss, then merged back into the reference — which leaves the nominal stack
untouched and stays inspectable when it fails. And generalization comes from
**environment diversity rather than episode length**: training across 99 paths
on multiple 3 km × 3 km terrains transfers to unseen environments better than
long-horizon training on a single 500 m terrain (8.89 cm against 10.41 cm
cross-track error), in about a third of the wall-clock time.

## Where this is going — integration with a VLA planner

The direction of the project is to bring all of this under a
**vision-language-action (VLA) planner**. The planner proposes a trajectory
from camera observations, ego history and navigation intent; Path2ST converts
that trajectory into controls the vehicle model can execute; the safety shield
constrains what the policy is allowed to do when a crossing conflict is
predicted; and the loop re-plans on each new observation.

<figure>
	<img src="/assets/images/projects/phys_vla_pipeline.svg">
  <figcaption>The planned end-to-end integration. Sensing and navigation intent go to the VLA planner, which emits a future trajectory on every new observation; Path2ST converts that trajectory into steering and throttle for the vehicle model; and the deterministic safety shield overrides the result with a STOP or PASS decision when a crossing conflict is predicted. The vehicle's new state becomes the next observation, and the planner re-plans.</figcaption>
</figure>

The separation of responsibilities is the point. **The planner proposes, the
controller tracks, and the shield enforces what must hold** — so that a large
learned model can supply intent and semantics without being trusted with the
guarantees, which stay in explicit, verifiable components. Dynamics alignment
is what makes that division safe to rely on: the controller and the shield
reason about a physics that has been calibrated against the real system rather
than an approximation of it.

{% capture programming %}
#### programming experience
Python, PyTorch, Genesis, differentiable simulation, Isaac Lab, Blender,
RL frameworks (PPO/QMIX), behavior cloning + residual RL, trajectory planning
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
