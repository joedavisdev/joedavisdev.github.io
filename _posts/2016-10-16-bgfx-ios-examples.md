---
layout: post
title:  "Running the bgfx examples on iOS"
date:   2016-10-16 23:00
excerpt: "A few tips to get the bgfx examples running on iOS"
categories: 3d-graphics
tags: [bgfx,3D graphics]
comments: true
---

I decided to take a look at the [bgfx](https://github.com/bkaradzic/bgfx) rendering library today, so I've pulled the source and deployed examples to a few platforms I have to hand. Ease of setup has varied, so I've been taking notes on the changes I had to make to get things running. I've pinged Branimir to find out how the official docs are built as I'd like to pull the advice into them at some point. In the meantime, you can find my notes below (based on the master branch pulled @ [6ff6cd6](https://github.com/bkaradzic/bgfx/commit/6ff6cd64958aadaac9b899f8f29392f026a2c83d)).

# OS X

Dead easy to setup. The [bgfx build instructions](https://bkaradzic.github.io/bgfx/build.html) cover most of it. Here's a summary for example-09-hdr:


* `$ cd $BGFX_ROOT`
* `$ ../bx/tools/bin/darwin/genie --with-examples --xcode=osx xcode4`
* `$ open .build/projects/xcode4-osx/bgfx.xcworkspace`
* Set the project's working directory to `${PROJECT_DIR}/../../../examples/runtime`
* Change macOS Deployment Target from default to 10.11
  * More of a problem with my setup/Xcode behaviour than bgfx. I'm running Xcode 8.0 (macOS 10.12 SDK) on a 10.11 machine. No idea why Xcode 8's default is a version OS X/macOS I'm not running...
* Select the example-09-hdr project & the device to run it on. Use the "Edit Scheme..." popup to set the working directory to `${PROJECT_DIR}/../../../examples/runtime` (required to load resources)
* Run!

# iOS

iOS was slightly more involved. As resources have to be packaged into the app bundle (can't read from a shared location on the file system like macOS), projects needed to be manually tweaked to get the examples running (already reported against bgfx as [#201](https://github.com/bkaradzic/bgfx/issues/201)). Here's a set up summary for example-09-hdr:

* `$ cd $BGFX_ROOT`
* `$ ../bx/tools/bin/darwin/genie --with-examples --xcode=ios xcode4`
* `$ open .build/projects/xcode4-ios/bgfx.xcworkspace`
* Fix code signing issues
* **Manual:** Add $BGFX_ROOT/examples/resources/* to the project with "Create folder references"
  * **Note:** This is a little excessive, as we're bundling resources for all examples instead of only packaging the resources we need. It's the quickest and easiest way to get it running though
  ![Step 1](/images/posts/20161016/1.png)
  ![Step 2](/images/posts/20161016/2.png)
  ![Step 3](/images/posts/20161016/3.png)
* Select the example-09-hdr project & the device to run it on
* Run!

I also hit an assert on iOS due to Apple's implementation of glInvalidateFramebuffer() not accepting the GL_DEPTH_STENCIL_ATTACHMENT enum. Resolving was a one liner (pull request [here](https://github.com/bkaradzic/bgfx/pull/951)).
