---
layout: post
title:  "Metal demos"
date:   2015-11-07 20:48
excerpt: An overview of the iOS Metal demos project I started a little while back
categories: 3d-graphics
tags: [dev diary,3D graphics,Metal,iOS]
comments: true
---

A few months ago when the developer community was getting excited about the arrival of DX12 and the promise of a cross-platform explicit graphics API in Vulkan, I thought I should finally get my hands dirty with something new. In addition to a Mac I also have a Metal-capable iOS device, so writing a few Metal demos seemed like a good place to start. A bonus for me is that I already know a lot about the GPUs in Apple's mobile devices, so I'm hoping it won't be too tricky for me to write optimal Metal code for them :)

According to GitHub it's been more than three months since my first [metal-demos](https://github.com/joedavisdev/metal-demos) repo commit...I'm hoping that if I blog about the project's progress, I'll guilt myself into dedicating more time to it!

## Getting started
Rather than writing everything from scratch I decided to use code from Apple's Metal SDK as a starting point. Very little rendering code is shared in Apple's demos. I suspect this is by design as the code should demonstrate how to interact with the API directly - not how to abstract it. Unlike the Apple SDK, one of the goals of my project is to abstract as much as possible into reusable helper classes. This should make it easier for my demos to manage buffers and avoid redundant Metal API calls.

My preferred programming language for the project would have been C++11, but Apple requires the API calls for their Frameworks to be issued from Swift or Objective-C code. I've opted to use Objective-C to interact with the API and C++ for everything else.

So - that's a quick overview of how I've approached the project. Here's a summary of what I've implemented so far:

## Current status

### 01_Basic3D
This is a modified version of Apple's MetalBasic3D demo. I've used the demo to validate my rendering helper classes as I've implemented them. Although this demo is working, I'll be tweaking it as I add more to the rendering abstraction layers. The demo code can be found [here](https://github.com/joedavisdev/metal-demos/tree/master/demos/01_Basic3D).

![cubes]({{url}}/images/posts/2015117/01_Basic3D.png)

### 02_BasicPODScene
Once I'd implemented the initial helper classes, the next logical step was to write a demo where assets (3D scenes, textures and shaders) are loaded from the app bundle. The [PowerVR Object Data (POD) format](http://community.imgtec.com/developers/powervr/tools/pvrgeopod/) is a binary container for cameras, lights, meshes and animations. I'm already familiar with it and it's well optimized (for example mesh data is sorted during POD generation to improve GPU cache efficiency), so it seemed like the right format for me to use.

I've used the PowerVR SDK's POD loading code rather than writing my own. Currently, the demo loads and renders a Stanford bunny model with a simple lighting effect.

![Stanford bunny]({{url}}/images/posts/2015117/02_BasicPODScene.png)

#### Todo

* Replace the naive mesh handling code with something more robust
* Load and apply textures to the mesh

The code for the demo can be found [here](https://github.com/joedavisdev/metal-demos/tree/master/demos/02_BasicPODScene).

## What's next?
There are a few tasks I'd like to complete before writing any new demos:

### JSON scene definition
In the current demos all scene components (pipelines, actors, lights, cameras, render targets etc.) are hard-coded. Moving these definitions to a structured format like JSON should make the rendering code more flexible.

### XCode project generation
I like XCode as an IDE, but I can't stand working with native XCode projects. They're a pain to diff and hand edit (unlike Visual Studio projects or Linux Makefiles), and I usually encounter issues upgrading when a new version of XCode is released. Moving to a project generator should simplify maintenance, particularly if I decide to add OS X support.

As I've used CMake for iOS before, I'll probably give that a go.
