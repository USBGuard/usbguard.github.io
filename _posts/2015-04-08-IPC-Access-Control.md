---
layout: post
title: "IPC interface access control"
date: 2015-04-08 19:30:59+02:00
comments: true
sitemap:
  lastmod: 2015-04-08 19:30:59+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

Today I have implemented a simple form of access control to the IPC interface of the USBGuard daemon. The [libqb](https://github.com/ClusterLabs/libqb) provides a callback slot for a function that decides whether to accept the IPC connection request or not. So implementing a DAC based ACL was a quite easy task and the feature will be part of the next release, usbguard-0.3.

The ACL is enabled by setting either the `IPCAllowUsers` or `IPCAllowGroups` configuration option in the *usbguard-daemon.conf* file. As the names suggest, it's possible to specify more than one user or group. Multiple items are expected to be separated by a space character. For example, setting:

    IPCAllowGroups=wheel

would allow users who are members of the *wheel* group to use the USBGuard IPC interface. I have made exactly this setting the default in the default distribution configuration file which is shipped in the packages available through the [Copr repository](https://copr.fedoraproject.org/coprs/mildew/usbguard/).

Implementing this feature also allowed me to finally [submit a request](https://bugzilla.redhat.com/show_bug.cgi?id=1209971) to include USBGuard as an official Fedora package. I didn't wanted to do that without either this ACL feature or the [planned public key authentication](https://github.com/dkopecek/usbguard/issues/8) as that would probably deter many potential users of the package -- they wouldn't like to run a program which allows anyone on the system to manipulate with USB device authorization.
