sap-netweaver-preconfigure
================

This role configures a RHEL 7 or RHEL 8 system according to applicable SAP notes so that SAP NetWeaver can be installed.

Requirements
------------

To use this role, your system needs to be installed according to:
- RHEL 7: SAP note 2002167, Red Hat Enterprise Linux 7.x: Installation and Upgrade, section "Installing Red Hat Enterprise Linux 7"
- RHEL 8: SAP note 2772999, Red Hat Enterprise Linux 8.x: Installation and Configuration, section "Installing Red Hat Enterprise Linux 8".
- Role sap-preconfigure should be run before using this role.

Role Variables
--------------

### required packages
The following variable contains the additional package which is required for SAP NetWeaver.
```yaml
sap_netweaver_preconfigure_packages
```

Example Playbook
----------------

Here is a simple playbook:

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
