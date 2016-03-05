---
layout: post
title:  "A few popular IMG blog posts"
date:   2016-03-05 10:46
excerpt: "A brief overview of some posts I've written for the Imagination Technologies blog over the years"
categories: 3d-graphics
tags: [3D graphics,PowerVR,OpenGL ES,Vulkan]
comments: true
---

I've posted technical articles to the Imagination Technologies blog sporadically over the last few years as I've found the time to write content. My most recent article received more attention than I expected so, in lieu of new content to post on this blog, I thought I'd cross reference a few IMG articles that still get a decent number of hits :)

## Why GPUs don’t like to share – a guide to improve your renderer on PowerVR-based platforms

![Texture orphaning/ghosting][image-1]

This article discusses the performance implications of modifying buffers and textures from the CPU-side while GPU read operations on those resources are still pending. The driver behaviour discussed is specific to PowerVR, but all GPU vendors have to deal with these problems (either by stalling the CPU when writes are issued or by orphaning/ghosting buffers).

You can find the full article [here][1].

## Understanding OpenGL ES: Multi-thread and multi-window rendering

![Multi-threaded resource uploads][image-2]

Multi-threaded rendering in OpenGL ES can be tricky. You have to carefully consider the type of work that can be issued to a background thread and ensure signals are sent to the primary thread when a resource is ready for use. It's also quite easy to shoot yourself in the foot and make performance worse if you naively call functions that are more costly than they seem, e.g. eglMakeCurrent().

In this article, I've listed a number of best practices for multi-thread and multi-window rendering in OpenGL ES. You can find the full article [here][2].

## Panel of graphics experts discusses Vulkan at the Khronos Paris chapter

![Vulkan][image-3]

At the end of January 2016, I attended the Khronos Paris Chapter's first meetup and took part in a panel discussion on the Khronos Group's new Vulkan graphics and compute API. It was an extremely useful event for me, as I've only been working with the API for a few months and still have a lot of learn about it. 

Following the event, I decided to write an overview of some of the talking points I found most interesting. You can find the full article [here][3].

[1]:http://blog.imgtec.com/powervr/how-to-improve-your-renderer-on-powervr-based-platforms
[2]:http://blog.imgtec.com/powervr/understanding-opengl-es-multi-thread-multi-window-rendering
[3]:http://blog.imgtec.com/powervr/panel-discusses-vulkan-khronos-paris-chapter

[image-1]:http://withimagination.imgtec.com/wp-content/uploads/2013/05/Why-GPUs-dont-like-to-share-01-texture-ghosting.jpg
[image-2]:http://withimagination.imgtec.com/wp-content/uploads/2014/11/OpenGL-data-upload-Optimized.png
[image-3]:http://blog.imgtec.com/wp-content/uploads/2015/10/VulkanLogo.png