---
layout: home
title: home
---

The USBGuard software framework helps to protect your computer against rogue USB devices (a.k.a. [BadUSB](https://srlabs.de/badusb)) by implementing basic whitelisting and blacklisting capabilities based on device attributes.

## Features

 * Rule language for writting USB device authorization policies
 * Daemon component with an IPC interface for dynamic interaction and policy enforcement
 * C++ API for interacting with the daemon component implemented in a shared library
 * A "oneshot" component for static, on-demand processing of the policy

## Supported Operating Systems

Currently, USBGuard works only on Linux. To enforce the user-defined policy, it uses the USB device authorization feature implemented in the Linux kernel since 2007. Read [this document](https://www.kernel.org/doc/Documentation/usb/authorization.txt) if you want to know more.
