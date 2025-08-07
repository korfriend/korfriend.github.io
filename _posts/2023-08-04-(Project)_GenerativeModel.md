---
title: "Deep Generative Model"
date: 2021-06-01 -0000
categories:
  - Projects
#tags:
#  - Generative Model
#  - AI
#  - StyleGAN
#  - NeRF

header:
  teaser: "/assets/images/deep_gm_teasor.jpg"
  image: "/assets/images/hairtransfer.jpg"
---
1. Controllable Image Generation with Lightweight Diffusion Models
Building on our past success in creating and manipulating novel hairstyles with [StyleGAN2](https://github.com/NVlabs/stylegan2), our research has now advanced to the next generation of generative models. We are currently focused on **developing lightweight, diffusion-based models for controllable image generation**. Our primary goal is to create highly efficient frameworks that enable intuitive, real-time image manipulation through simple user inputs, such as sketches or text prompts, while maintaining high-fidelity results. This research aims to make advanced content creation more accessible and interactive.

2. Real-time 3D Scene Reconstruction with Gaussian Splatting
In the realm of 3D scene representation, our focus has evolved towards the cutting-edge technique of 3D Gaussian Splatting. We are actively researching methods to achieve real-time, high-fidelity generation of large-scale indoor maps. Our work concentrates on optimizing the capture-to-render pipeline, enabling instant reconstruction and interactive exploration of complex environments. This technology is being developed for seamless integration into robotics, augmented reality (AR), and digital twin applications.

<figure class="third">
	<img src="/assets/images/class_dgm1.gif">
	<img src="/assets/images/nerf1.gif">
  <img src="/assets/images/nerf2.gif">
	<figcaption>Scene representation by NeRF. (images from NVIDIA)</figcaption>
</figure>

{% capture programming %}
#### programming experience
Python, Pytorch, Tensorflow
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>