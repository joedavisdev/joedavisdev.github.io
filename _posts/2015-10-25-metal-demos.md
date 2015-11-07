---
layout: post
title:  "Metal demos"
date:   2015-11-7 16:15
excerpt: An initial overview of my Metal demos project
categories: site-update
tags: [dev diary,3D graphics,Metal,iOS]
comments: true
---

Although I spend a lot of time debugging and profiling 3D graphics software, my expertise is very OpenGL/OpenGL ES focussed. I used DirectX a bit at university but haven't really touched it since I graduated. I suspect that's due to my day job being dominated by OpenGL ES and that I ditched my personal Windows desktop in favour of a Mac laptop ~2010. A few months ago when the developer community was getting excited about the arrival of DX12 and the promise of a cross-platform explicit graphics API in Vulkan, I thought I should finally get my hands dirty with something new. In addition to my Mac I also have a Metal-capable iOS device, so writing a few Metal demos seemed like a good place to start. A bonus for me is that I already know a lot about the GPUs in Apple's mobile devices, so I'm hoping it won't be too tricky for me to write optimal Metal code for them :)

According to GitHub it's been more than three months since my first [metal-demos](https://github.com/joedavisdev/metal-demos) repo commit...I'm hoping that if I blog about the project's progress, I'll guilt myself into dedicating more time to it!

## Current status

After downloading Apple's Metal SDK and hacking away at the examples I began incrementally abstracting functionality into a small set of helper classes. The aim of doing so was to create a common rendering layer I could use in all my demos. I wanted the option of reusing code later with other APIs (e.g. DX12 & Vulkan) so I've used C++ classes where possible. As Metal API calls can only be made from Swift or Objective-C, there isn't an awful lot of C++ code in the repo yet (excluding GLM etc. that I've checked in to the thirdParty directory).

To validate the helper classes, I integrated them into Apple's MetalBasic3D demo. My version of the demo is a somewhat moving target as I continue to tweak the helper classes. The latest revision of the demo can be found [here](https://github.com/joedavisdev/metal-demos/tree/master/demos/01_Basic3D).

The next step was to write a new demo using the helper classes. Rather than focusing on specific rendering techniques, I've chosen to implement a simple 3D mesh renderer in this second demo. As I'm familiar with the format and it's well optimised for run-time GPU cache access, I've chosen to use the [POD 3D scene format](http://community.imgtec.com/developers/powervr/tools/pvrgeopod/). The POD mesh rendering demo can be found [here](https://github.com/joedavisdev/metal-demos/tree/master/demos/02_BasicPODScene).

## What's next?
Before adding any new demos I'd like to refine and extend my helper classes. Tasks on my todo list include:

* JSON scene definition (pipelines, actors, cameras, render targets etc.)
	* This may take a while as I'll probably have to write a bunch of new helper classes
* XCode project generation
	* I'll probably use CMake for this, unless I find something better
	* I might add OS X Metal support if it doesn't seem too tricky. My Macbook Pro is too old to run Metal though, so I won't be able to test it...