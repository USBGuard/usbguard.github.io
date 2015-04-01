---
title: Compilation And Instalation
layout: page
---

If you want to compile the sources from a release tarball, you'll have to install development files for:

 * [libqb](https://github.com/ClusterLabs/libqb) - used for IPC
 * [libsodium](http://libsodium.org) - used for hashing
 * systemd-devel - used for udev

And then do:

    $ ./configure
    $ make
    $ sudo make install

If you want to compile the sources in a cloned repository, there's one additional step required:

	$ git submodule init
	$ git submodule update

This will fetch the sources of [cppformat](https://github.com/cppformat/cppformat), [json](https://github.com/nlohmann/json/)
and [spdlog](https://github.com/gabime/spdlog) which are used in this project too.

If you want to modify the lexer and/or the parser, you'll have to generate new source files for them. To learn how to do that, read [src/Library/RuleParser/README.md](src/Library/RuleParser/README.md).

## Pre-compiled packages

### Fedora Linux

Pre-compiled packages for Fedora 20, 21, 22 and rawhide are distributes using a Copr [repository](https://copr.fedoraproject.org/coprs/mildew/usbguard/).
You can install the repository by executing the following steps:

    $ sudo yum install yum-plugin-copr
    $ sudo yum copr enable mildew/usbguard
    $ sudo yum install usbguard

To actually start the daemon, use:

    $ sudo systemctl start usbguard.service
