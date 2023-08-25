---
#layout: splash
title: "Auto- Vehicle Asistantance Imaging"
date: 2022-07-01 -0000
categories:
  - Projects
#tags:
#  - Avikus
#  - Unreal Engine 5
#  - Computer Vision
#  - Graphics Simulation
header:
  teaser: "/assets/images/svm_teasor.jpg"
  image: "/assets/images/svm1.jpg"
  #overlay_color: "#EEEEEE"
  #overlay_filter: linear-gradient(rgba(85, 145, 197, 0.3), rgba(238, 238, 238, 0.3))
  #overlay_image: /assets/images/wordcloud5.png
  #actions:
  #  - label: "<i class='fas fa-thumbs-up'></i> Join us"
  #    url: "/docs/quick-start-guide/"
#excerpt:
#  Ready for professional for visual technology ?!
---
We have been interested in technology development that combines computer graphics and computer vision, and recently, we have been conducting the development of a three-dimensional surround view monitor (SVM) for ship docking.

>Traditional SVM systems have two critical issues. First, when projecting images obtained through RGB sensors, they do not consider the geometry of the three-dimensional space, resulting in a distorted top view that differs from the real-world top view. Second, problems such as ghosting can occur in overlapping areas due to the alignment of multiple images, which reduces the overall reliability of the SVM system. (Hyundai Motor)

These issues become even more critical in marine environments where the ground is not static, unlike roads. Therefore, we propose our network to address these issues by reconstructing the partial geometry with various AI technologies.

Due to the marine environment, data acquisition is limited and verification of the proposed algorithm is difficult. To resolve this, we have implemented **ship docking simulation through Unreal Engine 5 and developed a virtual sensor plugin**. Through the virtual sensor data captured in the simulation, we have been developing **a module that combines geometry-correction-based homography technology and various AI technologies of segmentation, inpainting, and super resolution**.

<figure class="half">
	<img src="/assets/images/svm2.jpg">
	<img src="/assets/images/svm4.jpg">
	<figcaption>SVM with inpainting, and our proposed method (suppressing the ghost artifact).</figcaption>
</figure>

{% include video id="1nOennz61whM59Irmfz7n-s2sASWFo1au" provider="google-drive" caption="UE-based simulation and SVM system"%}
<br>
{% include video id="1nOoUoPOVkLPSojvK4Ws2vEh0qUD3eUtX" provider="google-drive" caption="Ship navigation with undersea-terrain sensor visualization"%}

{% capture programming %}
#### programming experience
Unreal Engine plugin developement, Unreal Engine Blueprint/C++, Python, Tensorflow, Pytorch
{% endcapture %}

<div class="notice">{{ programming | markdownify }}</div>