---
layout: post
title:  "textureinfo"
date:   2016-05-19 21:30
excerpt: "Command-line utility to print PVR file header info"
categories: tools
tags: [dev diary,tools]
comments: true
---
I was after a tool recently to batch print PVR file header information, but couldn't spot anything suitable. As I've killed my rendering engine project and was looking for something smaller to work on I thought I may as well write my own.

`textureinfo` is a command-line utility that prints texture container header information to stdout. If the `--csv` flag is given, it'll dump the header info to a CSV file instead of printing it. The tool only supports PVR v3 containers right now, but I'll probably add a few more formats in the future.

The code is hosted on GitHub under an MIT licence [here](https://github.com/joedavisdev/textureinfo).

Makefiles/projects are generated via CMake.
