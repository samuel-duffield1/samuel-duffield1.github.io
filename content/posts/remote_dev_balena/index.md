---
title: "Accessing Docker Containers on Edge Compute Devices using Balena"
date: 2025-07-16
extra:
    toc: true
    math: true
---
Author: Sam Duffield

I've written an exmaple of how to setup an `openssh-server` on a `ubuntu:22.04` container on my personal github profile [here](https://github.com/samuel-duffield1/vscode-remote-dev-balena).

As noted in the `README.md`, I've found this useful for writing temporary/experimental hardware interface code to test drivers & hardware that would otherwise be unavailable to test on a desktop machine. This reduces the `Build->Test->Modify` loop that would otherwise be a little bit slower on an edge compute device, even with such things such as "Balena Livepush".

A couple of things to note in how this solution was designed:
1. `supervisor` was used to ensure concurrency of the `openssh-server` as a background process for any foreground process that may be running
2. A seperate port to `22` was used to avoid conflict with the HostOS container of Balena.
3. `rsync` is provided as a way to auto-sync back files from the remote device to the host machine (although for most simple tweaks, I find myself dragging & dropping files between 2 vscode instances on my 2 monitors).