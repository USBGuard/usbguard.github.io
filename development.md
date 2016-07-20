---
title: Development
layout: page
---

The USBGuard project uses github for tracking issues and the overall development process:

[https://github.com/dkopecek/usbguard/](https://github.com/dkopecek/usbguard/)

## Contribute

USBGuard is an open-source project and anyone can contribute to it. There are many ways one can contribute to the project -- source code, documentation enhancements, translations, artwork, etc. A nice summary of different ways to contribute is given in an article by Andy Lester, [14 Ways to Contribute to Open Source without Being a Programming Genius or a Rock Star](http://blog.smartbear.com/programming/14-ways-to-contribute-to-open-source-without-being-a-programming-genius-or-a-rock-star/).

### Reporting bugs or requesting features

If you'd like to report a bug or request a feature, please use the [issue tracker](https://github.com/dkopecek/usbguard/issues) or, if you don't have a GitHub account, send your report/request via e-mail to [dkopecek@redhat.com](mailto:dkopecek@redhat.com).

 * [Link to report a bug](https://github.com/dkopecek/usbguard/issues/new?labels=bug)
 * [Link to request a feature](https://github.com/dkopecek/usbguard/issues/new?labels=enhancement)

### Sending patches

If you don't have a GitHub account and therefore cannot [contribute your patches by forking the repository and creating a pull request](https://help.github.com/articles/using-pull-requests/), you can still send the patch via e-mail.

The preferred way to prepare the patch is to get fresh copy of the git repository:

    $ git clone https://github.com/dkopecek/usbguard

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

 * amenophobis
 * Beringer, Ian
 * Cowgill, James
 * Deppenwiese, Philipp
 * Kitt, Stephen
 * Kopeček, Daniel
 * Nicanor, Muri
 * Palmer, Rebecca N.
 * Sroka, Radovan
 * Stadelmann, Christian

**Thanks!**
