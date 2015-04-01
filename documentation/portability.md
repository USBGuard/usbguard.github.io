---
title: Portability
layout: page
---

Altought the primary target and development platform of this project is Linux, the code aims to be portable to other operating systems as well. Internally, the USBGuard daemon tries to abstract USB device handling as much as possible and for this purpose it uses two base classes that define the interface which the daemon uses for interacting with USB devices. A USB device is represented by the `usbguard::Device` class. The seconds class, `usbguard::DeviceManager`, defines an interface for USB device discovery and authorization. Please refer to the `usbguard::LinuxDevice` and `usbguard::LinuxDeviceManager` classes for an example implementation. More detailed documentation will be added as soon as possible.
