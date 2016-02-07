---
layout: home
title: home
---

The USBGuard software framework helps to protect your computer against rogue USB devices (a.k.a. [BadUSB](https://srlabs.de/badusb)) by implementing basic whitelisting and blacklisting capabilities based on device attributes.

## Features

 * [Rule language](documentation/rule-language.html) for writting USB device authorization policies
 * Daemon component with an IPC interface for dynamic interaction and policy enforcement
 * Command line and GUI interface to interact with a running USBGuard instance
 * C++ API for interacting with the daemon component implemented in a shared library

## Supported Operating Systems

Currently, USBGuard works only on Linux. To enforce the user-defined policy, it uses the USB device authorization feature implemented in the Linux kernel since 2007. Read [this document](https://www.kernel.org/doc/Documentation/usb/authorization.txt) if you want to know more.
