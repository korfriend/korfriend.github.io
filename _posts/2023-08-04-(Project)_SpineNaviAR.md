---
title: "AR Navigation-based Surgical Guidance System"
date: 2023-04-01 -0000
categories:
  - Projects
#tags:
#  - Augmented Reality
#  - Surgical Navigation
#  - Tracking
#  - Calibration
header:
  teaser: "/assets/images/ar_navi_teasor.jpg"
  image: "/assets/images/ar_navi1.jpg"
---
We have developed an **AR navigation-based surgical guidance system** that
augments a surgeon's view with intra-operative imaging and tool-tracking
information. Building on our experience from a large-scale
government-supported AR project — where we built efficient AR tracking and
calibration pipelines that integrated scans from multiple devices into a
single registered image — we extend this capability to the surgical setting,
where precision, robustness, and intuitive visualization are critical.

The system targets **simple surgical workflows** in which the surgical area
is captured by an **X-ray C-arm** and the resulting images are used to
project surgical tools and auxiliary surgical information into the user's
view. The goal is to deliver an AR navigation image that gives the surgeon
spatially registered guidance without disrupting the operative flow.

Within this project, we have been researching and developing the
following challenging components:

1. **Operationally easy X-ray view calibration**: Because continuous X-ray
   shooting is not allowed, we developed an automated, user-friendly
   calibration procedure tailored to the operational constraints.
2. **High-precision, occlusion-robust tool tracking**: A combined optical
   and non-optical tracking pipeline that delivers reliable tool poses
   even under partial occlusion in the surgical field.
3. **Patient-pose-aware information update**: Recognizing patient pose
   from RGB camera analysis and updating the surgical information layer
   accordingly.
4. **AR camera calibration using surgical tools**: Using the tracked
   surgical tools themselves as calibration targets for the AR camera,
   simplifying the in-room calibration procedure.
5. **Effective AR visualization**: Designing the on-view rendering of
   X-ray-derived surgical guidance so that it remains informative without
   overwhelming the surgeon's perception.

<figure>
	<img src="/assets/images/ar_navi2.jpg">
  <figcaption>AR calibration.</figcaption>
</figure>

<figure>
	<img src="/assets/images/ar_navi3.jpg">
  <figcaption>AR navigation for surgery.</figcaption>
</figure>

{% capture programming %}
#### programming experience
C++, Python, OpenCV, Graphics Engine APIs
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>
