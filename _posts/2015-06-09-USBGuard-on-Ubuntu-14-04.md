---
layout: post
title: How to install the USBGuard framework on Ubuntu 14.04
author: Daniel Kopeček <dkopecek@redhat.com>
date: 2015-06-09 00:17:00+02:00
comments: true
sitemap:
  lastmod: 2015-06-09 00:17:00+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

I've received several requests for help with installation of the USBGuard framework on Debian/Ubuntu based systems. I thought that the existing generic instruction ([Documentation/Installation](https://usbguard.github.io/documentation/compilation.html)) would work, but after I installed a virtual Ubuntu 14.04 machine to try them out myself, I found out that they might be hard to follow for users which are not used to compile and install upstream sources -- and search, compile and install sources of the required dependencies.

On Ubuntu 14.04, for example, there's no package for the sodium library. The available NaCL library can't be used because it lacks some of the high-level API that libsodium implements and which is used in USBGuard.

Therefore, I've decided to bundle the [qb](https://github.com/ClusterLabs/libqb) and [sodium](https://github.com/jedisct1/libsodium) libraries and added *./configure* options that allow to use the bundled libraries on systems, where they aren't available as installable packages. That should be, of course, an exception and the as soon as the libraries become available, you should recompile USBGuard to use the packaged version instead.

To make it easier still, I wrote a short how-to compile & install USBGuard for Ubuntu 14.04 users. It should work for other \*buntus and on Debian too, I hope -- please let me know, if that isn't true). The document needs some polishing and I will work on it further.

The most up-to-date version of the how-to can be found [here](https://github.com/dkopecek/usbguard/blob/master/doc/usbguard-on-ubuntu-14.04.md).
