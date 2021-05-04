---
layout: page
title: Panoptes - Infrastructure Camera Control
# description: a project with no image
img: /assets/img/panoptes.png
importance: 4
category: research
---

Steerable surveillance cameras offer a unique opportunity to support multiple vision applications simultaneously. However, state-of-art camera systems do not support this as they are often limited to one application per camera. We believe that we should break the one-to-one binding between the steerable camera and the application. By doing this we can quickly move the camera to a new view needed to support a different vision application. When done well, the scheduling algorithm can support a larger number of applications over an existing network of surveillance cameras. With this in mind we developed Panoptes, a technique that virtualizes a camera view and presents a different fixed view to different applications. A scheduler uses camera controls to move the camera appropriately providing the expected view for each application in a timely manner, minimizing the impact on application performance. Experiments with a live camera setup demonstrate that Panoptes can support multiple applications, capturing up to 80% more events of interest in a wide scene, compared to a fixed view camera.