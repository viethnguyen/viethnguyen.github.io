---
layout: page
title: Activity Sensing using Ceiling Photosensors
# description: a project with no image
img: /assets/img/vls.png
importance: 4
category: research
---

This project explores the feasibility of localizing and detecting activities of building occupants using visible light sensing across a mesh of light bulbs. Existing Visible Light activity sensing (VLS) techniques require either light sensors to be deployed on the floor or a person to carry a device. Our approach integrates photosensors with light bulbs and exploits the light reflected off the floor to achieve an entirely device-free and light source based system. This forms a mesh of virtual light barriers across networked lights to track shadows cast by occupants. The design employs a synchronization circuit that implements a time division signaling scheme to differentiate between light sources and a sensitive sensing circuit to detect small changes in weak reflections. Sensor readings are fed into indoor supervised tracking algorithms as well as occupancy and activity recognition classifiers. Our prototype uses modified off- the-shelf LED flood light bulbs and is installed in a typical office conference room. We evaluate the performance of our system in terms of localization, occupancy estimation and activity classification, and find a 0.89m median localization error as well as 93.7% and 93.78% occupancy and activity classification accuracy, respectively.