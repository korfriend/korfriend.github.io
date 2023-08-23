---
title: "AR Navigation System"
date: 2023-04-01 -0000
categories:
  - Projects
tags:
  - Native C++
  - Tracking
  - Calibration
header:
  teaser: "/assets/images/ar_navi_teasor.jpg"
  image: "/assets/images/ar_navi1.jpg"
---
One of the most important applications of augmented reality is navigation. We have experience in conducting a large-scale government-supported AR project, where we have successfully developed an efficient AR tracking and calibration system to integrate data scanned from various devices into a single image. We have the capability to develop technology that projects information acquired from various sensor data into a single image. 

Recently, we have been working on a project to **build a navigation system for simple surgery**. The surgical area is captured by **an X-ray system known as the C-arm, and images from this system should project surgical tools and auxiliary surgical information**. **The final navigation image will be displayed onto the user's view, i.e., augmented reality**. In this project, we are researching and developing the following challenging components:

1. Due to the X-rays, continuous shooting is not allowed; thus, we are develpoing an easy and automated X-ray view calibration process from an operational perspective,
2. High-precision/occlusion-free tool tracking through a combination of optical tracking and non-optical tracking data,
3. Recognizing the patient's pose through RGB camera image analysis and updating surgical information based on the pose information,
4. AR camera calibration using surgical tools,
5. Effective visualization of X-ray surgical navigation images onto the user's view.

<figure>
	<img src="/assets/images/ar_navi2.jpg">
  <figcaption>AR calibration.</figcaption>
</figure>

<figure>
	<img src="/assets/images/ar_navi3.jpg">
  <figcaption>AR navigation for surgery.</figcaption>
</figure>