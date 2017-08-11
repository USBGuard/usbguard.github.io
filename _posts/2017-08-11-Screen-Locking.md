---
layout: post
title: "Blocking USB devices while the screen is locked"
author: Daniel Kopeček <dkopecek@redhat.com>
date: 2017-08-11 10:00:00+02:00
tags: [blog, usbguard, USB, screen locker, security]
comments: true
sitemap:
  lastmod: 2017-08-11 10:00:00+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

Since the [0.7.0 release](https://github.com/dkopecek/usbguard/releases/tag/usbguard-0.7.0), it is possible to influence how an already running `usbguard-daemon` instance handles newly inserted USB devices.
The behaviour is defined by the value of the `InsertedDevicePolicy` runtime parameter and the default choice is to apply the policy rules to figure out whether to authorize the device or not.

The parameter can be read and modified via the usbguard CLI:

```
$ sudo usbguard get-parameter InsertedDevicePolicy
apply-policy
```

To change the policy to `block` use:

```
$ sudo usbguard set-parameter InsertedDevicePolicy block
```

Now try to insert a USB device and it won't be authorized even if there's a rule in your policy that says otherwise. Devices connected before the parameter value change aren't affected and remain in the same state.

Please note that for the examples below to work, you need to allow your desktop user to modify the USBGuard runtime parameters.
This can be done either with [USBGuard IPC access control](https://dkopecek.github.io/usbguard/blog/2017/IPC-Access-Control) or by giving sudo permissions to run `usbguard set-parameter` without authentication.

The following command will allow user **joe** to read and modify the runtime parameters via USBGuard IPC:

```
$ sudo usbguard add-user joe --parameters ALL
```

Note that the command will set the ACL exactly to what is specified on the command line, not append to the existing ACL settings for the user in case they exist.

## Blocking new USB device while the screen is locked

### Method #1: Screen locker wrapper script

If you are using a custom screen locker like `i3lock`, you'll need to create a wrapper script that takes care of setting the `InsertedDevicePolicy` parameter, something like this:

```
#!/bin/sh

POLICY_UNLOCKED=apply-policy
POLICY_LOCKED=reject

revert() {
  usbguard set-parameter InsertedDevicePolicy $POLICY_UNLOCKED
}

trap revert SIGHUP SIGINT SIGTERM
usbguard set-parameter InsertedDevicePolicy $POLICY_LOCKED
i3lock -n
revert
```

Now adjust your screen locker shortcuts and setting to point to this wrapper script instead of the original locker command and that's it.

### Method #2: D-Bus screen (un)lock signals

If you are using a desktop environment which has built-in screen locking support, then it probably signals the "screen (un)locked" state via D-Bus.
In that case you need to create a script to watch for these signals and set the `InsertedDevicePolicy` parameter appropriately.
The script should be running in your session (refer to your desktop environment's documentation on how to automatically start the script after you log in).

Example script:

```
#!/bin/sh

DBUS_INTERFACE=org.freedesktop.ScreenSaver
POLICY_UNLOCKED=apply-policy
POLICY_LOCKED=reject

dbus-monitor --session "type='signal',interface='"$DBUS_INTERFACE"'" |
  while read x; do
    case "$x" in 
      *"boolean true"*) usbguard set-parameter InsertedDevicePolicy $POLICY_LOCKED
    ;;
      *"boolean false"*) usbguard set-parameter InsertedDevicePolicy $POLICY_UNLOCKED
    ;;
    esac
  done
```
