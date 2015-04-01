---
title: Rule Language
layout: page
---

The USBGuard daemon decides which USB device to authorize based on a policy defined by a set of rules. When an USB device is inserted into the system, the daemon scans the existing rules sequentially and when a matching rule is found, it either authorizes (allows), deauthorizes (blocks) or removes (rejects) the device, based on the rule target. If no matching rule is found, the decision is based on an implicit default target. This implicit default is to block the device until a decision is made by the user.

The rule language grammar, expressed in a BNF-like syntax, is the following:

    rule ::= target device.

    target ::= "allow" | "block" | "reject".

    device ::= device_id device_attributes.
    device ::= .

    device_id ::= "*:*" | vendor_id ":*" | vendor_id ":" product_id.

    device_attributes ::= device_attributes | attribute.
    device_attributes ::= .

    attribute ::= name string.

## Targets

The target of a rule specifies whether the device will be authorized for use or not. Three types of target are recognized:

 * `allow` - authorize the device
 * `block` - deauthorize the device
 * `reject` - remove the device from the system

## Device specification

Except the target, all the other fields of a rule need not be specified. Such a minimal rule will match any device and allows the policy creator to write an explicit default target (there's an implicit one too, more on that later). However, if one want's to narrow the applicability of a rule to a set of devices or one device only, it's possible to do so with a device id and/or device attributes.

### Device ID

A USB device ID is the colon delimited pair *vendor\_id:product\_id*. All USB devices have this ID assigned by the manufacturer and it should uniquely identify a USB product. Both *vendor\_id* and *product\_id* are 16-bit numbers represented in hexadecimal base.

In the rule, it's possible to use an asterisk character to match either any device ID `*:*` or any product ID from a specific vendor, e.g. `1234:*`.

### Device attributes

(Please see [issue #11](https://github.com/dkopecek/usbguard/issues/11) and comment on the proposed changes related to this section)

Device attributes are specific value read from the USB device after it's inserted to the system. Which attributes are available is defined bellow. Some of the attributes are derived or based on attributes read directly from the device. The value of an attribute is represented as a double-quoted string.

List of attributes:

 * `class "NN"`
 * `hash "[0-9a-f]{32}"`
 * `name "..."`
 * `port "[0-9]{1,2}-[0-9]{1,2}"`
 * `port { "[0-9]{1,2}-[0-9]{1,2}" "[0-9]{1,2}-[0-9]{1,2}" ... }`
 
