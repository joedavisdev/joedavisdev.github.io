---
layout: post
title:  "Cross-vendor shader profiling"
date:   2016-07-17 22:31
excerpt: "An overview of existing shader profiling tools followed by an intro to my WIP browser-based shader profiler"
categories: tools
tags: [dev diary,tools]
comments: true
---

One of my most frequently used 3D graphics debugging and optimisation tools is [PVRShaderEditor](https://community.imgtec.com/developers/powervr/tools/pvrshadereditor). As you'd probably guess from the name, it's a shader editor for developers targeting PowerVR GPUs! In addition to the editor functionality you would expect (syntax highlighting, line numbers...text editing) it uses offline builds of the PowerVR shader compilers to generate errors, warnings and emulated cycle count performance statistics as you type. This turns the tedious process of verifying shader language and performance characteristics on-device into a core part of the authoring process. The tool runs on Windows, macOS and Linux which is handy for me as I regularly jump between all three :)

![The PVRShaderEditor interface](https://community.imgtec.com/wp-content/uploads/sites/2/2014/11/PVRShaderEditor_640x388.png)

A few years ago, Imagination went beyond the cycle counts and exposed shader disassembly for all Rogue GPUs (Series6 and newer). This has been a really handy feature as it gives transparency to the compilation process and makes GPU ALU behaviour much easier to understand.

Although the tool is already very useful, there are a few limitations I would love to see addressed in the future.

## Single active compiler

Currently, output is specific to a single active compiler. If you want to see how behaviour differs between GPU families, you have to manually toggle which compiler is active.

##  PowerVR only

Only PowerVR compilers are packaged with the tool. A future release will carry [glslangValidator](https://www.khronos.org/opengles/sdk/tools/Reference-Compiler), the Khronos group's reference compiler. I doubt a plugin interface will be added any time soon.

Imagination aren't the only GPU vendor with a tool like this, but I've always favoured it as PowerVR was my primary target and I could influence which bugs/feature requests were prioritised ;)
Now that I need to be worry about shader performance on multiple GPU architectures, it seemed like a good time to consider alternatives.

# Cross-vendor shader editor + profiler

So far, I'm only aware of one project that has attempted this. [Josh Barczak](https://twitter.com/JoshuaBarczak) from Firaxis wrote a nifty GUI tool called [Pyramid](https://github.com/jbarczak/Pyramid) that integrates the following compilers:

* HLSL
  * Microsoft D3D compiler - generates D3D assembly
  * AMD DXX driver - used for GCN disassembly and shader execution simulation
  * AMD CodeXL analyzer
* GLSL
  * Khronos reference glslang validator
  * Imagination PowerVR Rogue compiler
  * ARM Mali offline compiler
  * glsl-optimizer

![The Pyramid interface (GLSL)](https://raw.githubusercontent.com/jbarczak/Pyramid/master/doc/ui-glsl-powervr.png)

I've played around with it a few times and it does exactly what I need it to. I suspect it'll become an essential part of my workflow in the near future.

One limitation of Pyramid is that it's Windows only. With a little bit of fiddling, I'm sure it would work under Wine on macOS and Linux. As I was looking for a new hobby project though, I thought it could be fun to write a browser based tool that mimics Pyramid's functionality.

# Existing browser-based code editors

The project idea isn't particularly new. There are plenty of online code editors for C++ and GLSL. For example:

* C/C++
  * [cpp.sh](http://cpp.sh)
* GLSL
  * [Shadertoy](https://www.shadertoy.com)

Although browser-based editors exist, I haven't found an equivalent of PVRShaderEditor or Pyramid. Hopefully this means other people will find the tool I'm working on useful :)

# Writing my own GLSL editor + profiler

I've started my project with two prototypes - one for shader compilation, another for the GUI interface. Once I've got a better understanding of how I want those two components to work, I'll start writing the real thing.

Here's a screenshot of my current GUI prototype:

![GLSL online prototype](/images/posts/20160717/glslonline_prototype.png)

In my next post, I'll overview my prototypes and will explain which libraries/technologies I've decided to use for the project.
