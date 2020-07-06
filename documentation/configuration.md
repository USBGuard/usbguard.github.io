---
title: Configuration
layout: page
---

## usbguard-daemon.conf -- USBGuard daemon configuration file

The `usbguard-daemon.conf` file is loaded by the USBGuard daemon after it parses its command-line options and is used to configure runtime parameters of the daemon. The default search path is _/etc/usbguard/usbguard-daemon.conf_. It may be overridden using the `-c` command-line option, see usbguard-daemon(8) for further details.

### Options

 * `RuleFile=<path>`
   The USBGuard daemon will use this file to load the policy rule set from it and to write new rules received via the IPC interface.
   Default: `%sysconfdir%/usbguard/rules.conf`

 * `ImplicitPolicyTarget=<target>`
   How to treat devices that don't match any rule in the policy.
    * allow - authorize the device
    * block - deauthorize the device
    * reject - logically remove the device node from the system
   `Default: block`

 * `PresentDevicePolicy=<policy>`
   How to treat devices that are already connected when the daemon starts:
    * allow - authorize every present device
    * block - deauthorize every present device
    * reject - remove every present device
    * keep - just sync the internal state and leave it
    * apply-policy - evaluate the ruleset for every present device
   Default: `apply-policy`

 * `PresentControllerPolicy=<policy>`
   How to treat USB controllers that are already connected when the daemon starts:
    * allow - authorize every present device
    * block - deauthorize every present device
    * reject - remove every present device
    * keep - just sync the internal state and leave it
    * apply-policy - evaluate the ruleset for every present device
   Default: `keep`

 * `InsertedDevicePolicy=<policy>`
   How to treat USB devices that are already connected after the daemon starts. One of block, reject, apply-policy.
   Default: `apply-policy`

 * `RestoreControllerDeviceState=<boolean>`
   The USBGuard daemon modifies some attributes of controller devices like the default authorization state of new child device instances. Using this setting, you can control whether the daemon will try to restore the attribute values to the state before modification on shutdown.

 * `DeviceManagerBackend=<backend>`
   Which device manager backend implementation to use.
   Backend should be one of uevent (default) or umockdev.

 * `IPCAllowedUsers=<username> [<username> ...]`
   A space delimited list of usernames that the daemon will accept IPC connections from.
   Default: `root`

 * `IPCAllowedGroups=<groupname> [<groupname> ...]`
   A space delimited list of groupnames that the daemon will accept IPC connections from.

 * `IPCAccessControlFiles=<path>`
   The files at this location will be interpreted by the daemon as IPC access control definition files. See the `<<ipc-access-control,IPC ACCESS CONTROL>>` section for more details.

 * `DeviceRulesWithPort=<boolean>`
   Generate device specific rules including the "via-port" attribute.
   Default: `false`

 * `AuditBackend=<backend>`
   USBGuard audit events log backend. The backend value should be one of FileAudit or LinuxAudit.
   Default: `FileAudit`

 * `AuditFilePath=<filepath>`
   USBGuard audit events log file path. Required if AuditBackend is set to FileAudit.
   Default: `%localstatedir%/log/usbguard/usbguard-audit.log`

 * `HidePII=<boolean>`
     Hides personally identifiable information such as device serial numbers and
     hashes of descriptors (which include the serial number) from audit entries.
     Default: false

## Security Considerations

### IPC

The daemon provides the USBGuard public IPC interface. Depending on your distribution defaults, access to this interface is limited to a certain group or a specific user only. Please set either the _IPCAllowedUsers_, _IPCAllowedGroups_ or _IPCAccessControlFiles_ options to limit access to the IPC interface. *Do not leave the ACL unconfigured as that will expose the IPC interface to all local users and will allow them to manipulate the authorization state of USB devices and modify the USBGuard policy.*

### RestoreControllerDeviceState configuration option

If set to true, the USB authorization policy could be bypassed by performing some sort of attack on the daemon (via a local exploit or via a USB device) to make it shutdown and restore to the operating-system default state (known to be permissive).

## IPC ACCESS CONTROL

Access to the USBGuard IPC interface can be limited per user or group. Furthermore, by using the IPC Access Control files, it is possible to limit the access down to the level of Sections and Privileges as explained below.

### Recommended: _IPCAccessControlFiles_

When you set _IPCAccessControlFiles_ option, the daemon will look for IPC access control files in the directory specified by the setting value. Each file in the directory is processed as follows:

 1. The basename of the file is interpreted as an username, UID, groupname or GID. If the names starts with `:` (colon), it is assumed that the rest of the name represents a group identifier (groupname or GID in case of a numeric-only string). Otherwise, it is interpreted as an user identifier (username or UID in case of numeric-only string).

 2. The contents of the file are parsed as `Section=privilege [privilege ...]` formatted lines which specify the section privileges. If a section is omitted, it is assumed that no privileges are given for that section.

Available sections and privileges:

 * `Devices`
   * modify: Change authorization state of devices including permanent changes (i.e. modification of device specific rules in the policy).
   * list: Ability to get a list of recognized devices and their attributes.
   * listen: Listen to device presence and device policy changes.

 * `Policy`
   * modify: Append rules to or remove any rules from the policy.
   * list: Ability to view the currently enforced policy.

 * `Exceptions`
   * listen: Receive exception messages.

 * `Parameters`
   * modify: Set values of run-time parameters.
   * list: Get values of run-time parameters.

The following is a generally usable and reasonably safe example of an access control file. It allows to modify USB device authorization state (`Devices=modify`), list USB devices (`Devices=list`), listen to USB device related events (`Devices=listen`), list USB authorization policy rules (`Policy=list`) and listen to exception events (`Exceptions=listen`):

    Devices=modify list listen
    Policy=list
    Exceptions=listen

Instead of creating the access control files by yourself, you can use the `usbguard add-user` or `usbguard remove-user` CLI commands. See usbguard(1) for more details.

### Legacy: _IPCAllowedUsers_ and _IPCAllowedGroups_

Example configuration allowing full IPC access to users _root_, _joe_ and members of the group _wheel_:

    IPCAllowedUsers=root joe
    IPCAllowedGroups=wheel
