---
layout: post
title:  "PowerVR Tools cleanup script"
date:   2015-12-20 15:20
excerpt: A Python script that removes PowerVR Tools binaries you may not want to keep
tags: [PowerVR SDK]
comments: true
---

The 3rd party installer we've been using for the last few years of PowerVR SDK releases does the job, but it's not without it's flaws. One of the engineers in the team started working on an alternative which is much more flexible. Unfortunately, we ran out of time to finish and test it for our 4.0 SDK release.

One of my biggest gripes with the current installer is that it installs PowerVR Tools binaries for every supported OS, even if you don't want them:

* Linux\_x86\_32
* Linux\_x86\_64
* OSX\_x86
* Windows\_x86\_32
* Windows\_x86\_64

This wastes a lot of disk space as the tools binaries are pretty big (~1GB per OS + bits combo). To combat this, I've written a simple Python script that removes all of the binaries you don't need.

<script src="https://gist.github.com/joedavisdev/4b4b1d0e473673ee204a.js"></script>

Hopefully we will have moved to the new installer when our 4.1 SDK is released (~March 2016). For now though, this script may help others that don't want to keep binaries for every OS around!
