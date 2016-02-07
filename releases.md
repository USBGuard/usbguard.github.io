---
title: Releases
layout: releases
date: 2016-02-08 00:00:00+02:00
comments: false
sitemap:
  lastmod: 2016-02-08 12:00:00+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

The latest release of usbguard is [**usbguard-0.4**](https://dkopecek.github.io/usbguard/dist/usbguard-0.4.tar.gz).

The latest release of usbguard-applet-qt is [**usbguard-applet-qt-0.3**](https://dkopecek.github.io/usbguard/dist/usbguard-applet-qt-0.3.tar.gz).

### usbguard-0.4

Download: [usbguard-0.4.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.4.tar.gz)

#### Major Changes

 * The daemon is now capable of dropping process capabilities and uses a seccomp based syscall whitelist. Options to enable these features were added to the usbguard-daemon command.
 * Devices connected at the start of the daemon are now recognized and the DevicePresent signal is sent for each of them.
 * New configuration options for setting the implicit policy target and how to handle the present devices are now available.
 * String values read from the device are now properly escaped and length limits on these values are enforced.
 * The library API was extended with the Device and DeviceManager classes.
 * Implemented the usbguard CLI, see usbguard(1) for available commands.
 * Initial authorization policies can be now easily generated using the `usbguard generate-policy` command.
 * Extended the rule language with rule conditions. See usbguard-rules.conf(5) for details.
 * Moved logging code into the shared library. You can use static methods of the Logger class to configure logging behaviour.
 * Removed the bundled libsodium and libqb libraries.
 * Fixed several bugs.
 * Resolved issues: #46, #45, #41, #40, #37, #32, #31, #28, #25, #24, #21, #16, #13, #9, #4

##### **WARNING**: Backwards incompatible changes

 * The device hashing procedure was altered and generates different hash values. If you are using the hash attribute in your rules, you'll have to update the values.
 * The bundled libsodium and libqb were removed. You'll have to compile and install them separately if your distribution doesn't provide them as packages.

### usbguard-0.3p3

Download: [usbguard-0.3p3.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.3p3.tar.gz)

#### Major Changes

 * use `AC_CHECK_HEADER` instead of a pkg-config based check for json and spdlog 
 * make check target available

### usbguard-0.3p2

Download: [usbguard-0.3p2.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.3p2.tar.gz)

#### Major Changes

 * Added configure script options to compile usbguard with system-wide json and spdlog libraries

### usbguard-0.3p1

Download: [usbguard-0.3p1.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.3p1.tar.gz)

#### Major Changes

 * Removed the bundled cppformat library

### usbguard-0.3, usbguard-applet-qt-0.3

Download: [usbguard-0.3.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.3.tar.gz), [usbguard-applet-qt-0.3.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-applet-qt-0.3.tar.gz)

#### Major Changes

 * Fixed appending of permanent rules
 * Implemented a DAC based IPC access control
 * Ship man pages for usbguard-daemon, usbguard-daemon.conf and usbguard-rules.conf
 * Ship the LICENSE file
 * Fixed distribution RPM spec file. Thanks to Petr Lautrbach and Ralf Corsepius for review.
 * Resolved issues: #18 #19 #13 

#### Updating

If you are using the USBGuard Copr repository, run:

    $ sudo yum update usbguard usbguard-applet-qt

Additionally, if the user under which you are running _usbguard-applet-qt_ isn't in the _wheel_ group, you should either add him to that group or change the ACL in _/etc/usbguard/usbguard-daemon.conf_ in order to be able to use the applet.

### usbguard-0.2, usbguard-applet-qt-0.2

Download: [usbguard-0.2.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-0.2.tar.gz), [usbguard-applet-qt-0.2.tar.gz](https://dkopecek.github.io/usbguard/dist/usbguard-applet-qt-0.2.tar.gz)

#### Major Changes

 * Support for modifying permanent rules over the IPC interface.
 * Reworked device hashing.
 * Rule language changes
   * set operators
   * renamed "port" to "via-port"
   * added "with-interface" matching attribute
   * removed the "class" attribute
 * The IPCClient, ConfigFile, Rule and RuleSet classes are now shipped in a shared library.
 * Created abstract interface for OS specific USB device handling.
 * Changed default daemon config path to /etc/usbguard/usbguard-daemon.conf.
 * Implemented basic USB descriptor structure parsing and improved interface type handling
 * The IPC API was changed:
  * added new signal, DevicePresent, which signals that a device was already present at the start of the IPC session
  * the DeviceInserted and DevicePresent signals pass interface types that the device supports
  * the explicit string arguments of the signals are now passed as a map
 * Resolved issues: #1 #2 #5 #6 #10 #11 

#### Updating

Note that the rule language syntax changed. USBGuard no longer recognizes the "class" attribute, which was removed, and the "port" attribute, which was renamed to "via-port".

If you are using the USBGuard Copr repository, run:

    $ sudo yum update usbguard usbguard-applet-qt

