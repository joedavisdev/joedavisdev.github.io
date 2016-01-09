---
layout: post
title:  "Initial components of an explicit rendering engine"
date:   2016-01-08 21:57
excerpt: "metal-demos: Initial components of an explicit rendering engine"
categories: 3d-graphics
tags: [dev diary,3D graphics,Metal,iOS]
comments: true
---
As discussed in my [last post](/posts/2015/11/07/metal-demos/), I've been tinkering with Apple's Metal API in my spare time to learn more about explicit graphics APIs. The holidays gave me a chance to dive back into the project, so it seemed like a good time to share a status update.

I've been using the 02_BasicPODScene demo to test code. I'm hoping the overview below will make sense without lots of snippets. In case you're interested though, you can find the most relevant bits of code in [gfx_device.h], [scene_man.hpp] and [BasicPODScene.mm].

[gfx_device.h]: https://github.com/joedavisdev/metal-demos/blob/develop/engine/renderer/inc/gfx_device.h
[scene_man.hpp]: https://github.com/joedavisdev/metal-demos/blob/develop/engine/core/inc/scene_man.hpp
[BasicPODScene.mm]: https://github.com/joedavisdev/metal-demos/blob/develop/demos/02_BasicPODScene/src/BasicPODScene.mm

# Current status

While reviewing the project's code, it became obvious that the existing graphics abstraction classes weren't particularly useful. So, I decided to design a cleaner graphics API abstraction layer and scene manager/renderer. The following overview is based on the code up to commit [b0c02cd](https://github.com/joedavisdev/metal-demos/commit/b0c02cd1ae9a87c6a95428d1738ef8db9a46e4f2).

## API abstraction
The GFX namespace (`gfx_device.h`) provides a C++ interface for Metal API calls. All Metal function calls are implemented in `metal_device.mm`. So far classes have been added for:

* Pixel formats (`GFX::PixelFormat`)
* Buffers (`GFX::Buffer`)
* Effects (`GFX::Effect` - vertex function & fragment function pointers)
* Shader libraries (`GFX::Library`)
* Pipeline descriptors (`GFX::PipelineDesc`)
* Pipeline state (`GFX::PipelineState`)

More classes will be added as the scene manager functionality is fleshed out. Hopefully, the `gfx_device.h` abstraction will be generic enough that it can be used as a starting point for Vulkan & DX12 back-ends in the future.

## Scene manager
The SceneMan class is responsible for loading the scene into memory and then to Metal. It utilizes GFX namespace classes to upload data to the graphics API, bake state and submit command buffers.

### Scene loading
Scene's are described with a JSON file like this one:

<script src="https://gist.github.com/joedavisdev/265d49936c708ddebd6a.js"></script>

Scene loading consists of the following actions:

* Parse the JSON file
* Load effects
    * Effect name, vertex shader name & fragment shader name
* Load actors
    * Position, model & effect
    * (If a [POD scene](https://community.imgtec.com/developers/powervr/tools/pvrgeopod/) model isn't already cached, it's loaded at this point)
* Load render passes
    * Attachment properties and a Regular Expression for the names of actors that should be rendered
* Build pipelines
    * Creates Metal pipeline descriptors from the render pass, actor and effect data (`GFX::PipelineDesc`)

Essentially, these steps track which resources have been loaded already and load resources if they're not already cached.

### Render pass baking
Once the scene has been loaded, graphics state can be baked. Baking currently consists of the following stages:

* Bake effects
    * Load an effect's vertex and fragment function pointers from the default library
* Bake pipelines
    * Loop through all built pipeline descriptors and bake state for each

# What’s next?

## Uniform buffers
Need to be created and populated. I'll probably create one per-actor initially, but could try and do something fancier later like batching them.

## Shader layouts
Ensure the attribute and uniform layouts used in shaders match the layout of buffers attached to draws.

## Other bits of state
Depth state, blend modes etc. May hard-code some defaults for now (e.g. always depth test & only render opaque objects).

## Command buffer baking
Once I've completed the tasks above, I should be able to start baking command buffers and drawing objects.

## Anything else?
Loads of stuff, including texture loading. The four tasks above will probably keep me busy for a while though :)
