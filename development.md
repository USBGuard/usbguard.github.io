---
title: Development
layout: page
---

The USBGuard project uses github for tracking issues and the overall development process:

[https://github.com/dkopecek/usbguard/](https://github.com/dkopecek/usbguard/)

The Qt applet repository is located at:

[https://github.com/dkopecek/usbguard-applet-qt/](https://github.com/dkopecek/usbguard-applet-qt/)

## Contribute

USBGuard is an open-source project and anyone can contribute to it. There are many ways one can contribute to the project -- source code, documentation enhancements, translations, artwork, etc. A nice summary of different ways to contribute is given in an article by Andy Lester, [14 Ways to Contribute to Open Source without Being a Programming Genius or a Rock Star](http://blog.smartbear.com/programming/14-ways-to-contribute-to-open-source-without-being-a-programming-genius-or-a-rock-star/).

### Sending patches

If you don't have a GitHub account and therefore cannot [contribute your patches by forking the repository and creating a pull request](https://help.github.com/articles/using-pull-requests/), you can still send the patch via e-mail.

The preferred way to prepare the patch is to get fresh copy of the git repository:

    $ git clone https://github.com/dkopecek/usbguard

or

    $ git clone https://github.com/dkopecek/usbguard-applet-qt

commit the change locally and use:

    $ git-format-patch -1 commit-id

to export the patch. commit-id is the commit number of the checkin you want to send (use `git log` to see it).

In the commit message, please state:

 * What changed
 * Why it changed
 * If the change is related to a tracked issue, include a reference to it.

### License

USBGuard is [licensed under the **GPLv2**](/usbguard/license). **By submitting a patch for inclusion in the USBGuard project, you are agreeing to license your changes under the GPLv2**.

### List of Contributors

The following list contains names of individuals, sorted by the last name, who are actively working on the project or contributed in some way to the project:

 * Kitt, Stephen
 * Kopeček, Daniel

**Thanks!**
