---
title: Compilation And Instalation
layout: page
---

If you want to compile the sources from a release tarball, you'll have to install development files for:

 * [libqb](https://github.com/ClusterLabs/libqb) - used for IPC
 * [libsodium](http://libsodium.org) - used for hashing
 * systemd-devel - used for udev

Optionally, you may want to install:

 * [libseccomp](https://github.com/seccomp/libseccomp) - used to implement a syscall whitelist
 * [libcap-ng](https://people.redhat.com/sgrubb/libcap-ng/) - used to drop process capabalities

And then do:

    $ ./configure
    $ make
    $ sudo make install

After the sources are successfully built, you can run the testsuite by executing:

    $ make check

If you want to compile the sources in a cloned repository, there are additional step required:

    $ git submodule init
    $ git submodule update

This will fetch the sources of [json](https://github.com/nlohmann/json/), [spdlog](https://github.com/gabime/spdlog) and [Catch](https://github.com/philsquared/Catch) which are used in this project too.

And to generate the *configure* script, run:

    $ ./autogen.sh

If you want to modify the lexer and/or the parser, you'll have to generate new source files for them. To learn how to do that, read [src/Library/RuleParser/README.md](https://github.com/dkopecek/usbguard/blob/master/src/Library/RuleParser/README.md).

## Pre-compiled packages

### Fedora Linux, RHEL or CentOS

Pre-compiled packages for Fedora 20, 21, 22, rawhide and EPEL 7 (RHEL, CentOS) are distributes using a Copr [repository](https://copr.fedoraproject.org/coprs/mildew/usbguard/).
You can install the repository by executing the following steps:

    $ sudo yum install yum-plugin-copr
    $ sudo yum copr enable mildew/usbguard
    $ sudo yum install usbguard
    $ sudo yum install usbguard-applet-qt

To actually start the daemon, use:

    $ sudo systemctl start usbguard.service
    $ usbguard-applet-qt
