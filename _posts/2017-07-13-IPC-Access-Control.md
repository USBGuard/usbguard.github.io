---
layout: post
title: "IPC interface access control"
author: Daniel Kopeček <dkopecek@redhat.com>
date: 2017-07-13 10:00:00+02:00
tags: [blog, usbguard, IPC, ACL]
comments: true
sitemap:
  lastmod: 2017-07-13 10:00:00+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

I have already covered how to configure `usbguard-daemon` IPC access control in a [previous post](https://dkopecek.github.io/usbguard//blog/2015/IPC-Access-Control).
However, the [0.7.0 release](https://github.com/dkopecek/usbguard/releases/tag/usbguard-0.7.0) introduced another way to configure the same thing with more control over who can do what.

Previously, one could only enable a user or group to use the whole IPC interface.
With the new ACL system, the access can be limited to specific sections of the interface and specific privileges inside that section.

The available sections and privileges are:

 * Section: **Devices**
    * `modify`: Change authorization  state  of  devices  including
permanent  changes (i.e. modification of device specific rules in
the policy).
    * `list`: Ability to get a list of recognized devices and their
attributes.
    * `listen`: Listen  to  device  presence  and  device  policy
changes.
 * Section: **Policy**
    * `modify`: Append rules to or remove any rules from the  poli‐
cy.
    * `list`: Ability to view the currently enforced policy.
 * Section: **Exceptions**
    * `listen`: Receive exception messages.
 * Section: **Parameters**
    * `modify`: Set values of run‐time parameters.
    * `list`: Get values of run‐time parameters.

To use this new system, you first have to modify the usbguard-daemon configuration and set the `IPCAccessControlFiles` setting to point to a location where the ACL definition files will be stored, for example: `/etc/usbguard/IPCAccessControl.d/`.

Once set, you can use the usbguard CLI to define the ACL. For example:

    $ sudo usbguard add-user joe --devices ALL --policy list,listen --exceptions ALL

That command will enable user `joe` to have full access to the `Devices` and `Exceptions` sections. In addition, `joe` will be able to list the policy and listen to policy signals.

To remove the definition, use:

    $ sudo usbguard remove-user joe


