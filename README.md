sap-netweaver-preconfigure
================

This role configures a RHEL 7 or RHEL 8 system according to applicable SAP notes so that SAP NetWeaver can be installed.

Requirements
------------

To use this role, your system needs to be installed according to:
- RHEL 7: SAP note 2002167, Red Hat Enterprise Linux 7.x: Installation and Upgrade, section "Installing Red Hat Enterprise Linux 7"
- RHEL 8: SAP note 2772999, Red Hat Enterprise Linux 8.x: Installation and Configuration, section "Installing Red Hat Enterprise Linux 8".
- Role sap-preconfigure should be run first.

Note
----
As per SAP notes 2002167 and 2772999, the role will switch to tuned profile sap-netweaver no matter if another tuned profile (e.g. virtual-guest) had been active before or not.

The role can check if enough swap space as per the prerequisite checker in sapinst has been configured on the managed node. Please check the SAP NetWeaver installation guide for swap space requirements.

Please do not run this role against a productive SAP NetWeaver system. The role will unconditionally make changes to the managed node, which might not be intended on productive SAP NetWeaver systems.

Role Variables
--------------

### Fail if there is less than 20480 MB of swap space configured
If the following variable is set to no, the role will not fail if less than 20480 MB of swap space is configured. Default is yes.
```yaml
sap_netweaver_preconfigure_fail_if_not_enough_swap_space_configured
```

Example Playbook
----------------

Here is a simple playbook which will configure a RHEL system for installation of SAP NetWeaver:

```yaml
---
    - hosts: all
      roles:
         - role: sap-preconfigure
         - role: sap-netweaver-preconfigure

...
```

License
-------

GNU General Public License v3.0

Author Information
------------------

Bernd Finger
