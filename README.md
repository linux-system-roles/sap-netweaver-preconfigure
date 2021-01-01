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

Do not run this role against an SAP NetWeaver or other production system. The role will enforce a certain configuration on the managed node(s), which might not be intended.

Role Variables
--------------

### Execute only certain steps of SAP notes
If the following variable is set to no, only the installion or configuration steps of SAP notes will be executed or checked. If this variable is undefined or set to no, all installation and configuration steps of applicable SAP notes will be executed.
```yaml
sap_netweaver_preconfigure_config_all
```

### Perform installation or configuration steps, or both
If you have set `sap_netweaver_preconfigure_config_all` (see above) to `no`, you can limit the scope of the role to only execute the installation or the configuration steps. For this purpose, set one of the following variables, or both, to `yes`. The default for both is `no`.
```yaml
sap_netweaver_preconfigure_installation
sap_netweaver_preconfigure_configuration
```

### Install required packages for Adobe Document Services
If the following variable is set to `yes`, required packages for Adobe Document Services according to SAP note 2135057 (RHEL 7) or 2920407 (RHEL 8) will be installed. Default is `no`.
```yaml
sap_netweaver_preconfigure_use_adobe_doc_services
```

### Run the role in assert mode
If the following variable is set to `yes`, the role will only check if the configuration of the managed node(s) is according to the applicable SAP notes. Default is `no`.
```yaml
sap_netweaver_preconfigure_assert
```

### Behavior of the role in assert mode
If the role is run in assert mode (see above) and the following variable is set to `yes`, assertion errors will not cause the role to fail. This can be useful for creating reports.
Default is `no`, meaning that the role will fail for any assertion error which is discovered. This variable has no meaning if the role is not run in assert mode.
```yaml
sap_netweaver_preconfigure_assert_ignore_errors
```

### Swap space for SAP NetWeaver
When installing SAP NetWeaver, the prerequisite checker verifies if enough swap space is configured. By default, the role checks is there is at least 20480 MB of swap space available.
This variable can be used set to the swap space limit to any other value.
```yaml
sap_netweaver_preconfigure_min_swap_space_mb
```

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
