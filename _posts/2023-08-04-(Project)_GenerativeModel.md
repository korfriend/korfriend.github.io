---
title: "Deep Generative Model"
date: 2021-06-01 -0000
categories:
  - Projects
tags:
  - Generative Model
  - AI
  - StyleGAN
  - NeRF

header:
  teaser: "/assets/images/wordcloud.png"
---
We are currently working on a project to create new hairstyles using the trained generator of [StyleGAN2](https://github.com/NVlabs/stylegan2). For this purpose, we're embedding features from various reference images and applying a loss for natural style transition. We are researching **techniques to propose seamless blending between the naturally generated style image and the original image**. Additionally, we are developing an **efficient hairstyle creation solution through various parametric encoding learning models for interactive style control using sketches and through the configuration of conditional style transition models**.
We are also conducting research on improvements to [NeRF](https://github.com/bmild/nerf), a neural network-based scene representation model, specifically for **few-shot cases and dynamic scene cases**. We are currently working to enhance the efficiency of our research through the NeRF plugin module of the rendering engine that our laboratory has been developing.