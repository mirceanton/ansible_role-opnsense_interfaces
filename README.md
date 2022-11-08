OPNsense: Interfaces
====================

An Ansible role that configures the interfaces on an opnSense firewall.

Requirements
------------

This role requires the `lxml` python package to be installed on the host system.

Role Variables
--------------

|              Variable               |     Type     |                                                                       Description                                                                        |
| :---------------------------------: | :----------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: |
|         opnsense_interfaces         | list(object) |                                             List of configuration settings for each interface individually.                                              |
|     opnsense_interfaces[].name      |    string    |                                                           The name for the network interface.                                                            |
|  opnsense_interfaces[].description  |    string    |                                           A short description for clarification, if the name does not suffice.                                           |
|     opnsense_interfaces[].iface     |    string    |                                                The name of the actual physical interface this is tied to.                                                |
|    opnsense_interfaces[].enabled    |    string    |                                        Disable the interface without needing to remove its assignment altogether.                                        |
|     opnsense_interfaces[].lock      |    string    |                                                 Whether or not to lock the settings for this interface.                                                  |
|    opnsense_interfaces[].address    |    string    |                                                         The address to assign to this interface.                                                         |
|    opnsense_interfaces[].subnet     |    string    |                                                                    The subnet length.                                                                    |
|    opnsense_interfaces[].gateway    |    string    |                                                             The gateway for this interface.                                                              |
| opnsense_interfaces[].block_private |    string    |              Block traffic claiming to come from private addresses. On WAN interfaces, this kind of traffic should not happen legitimately.              |
|  opnsense_interfaces[].block_bogon  |    string    | Block traffic claiming to come from invalid or reserved addresses (Martian packets). Note that this also includes multicast traffic using OSPF and RTMP. |

Dependencies
------------

N/A.

Example Playbook
----------------

```yaml
- name: Configure the interfaces on all firewalls
  hosts: opnsense

  roles:
    - role: mirceanton.opnsense_interfaces
      vars:
        opnsense_interfaces:
          - name: wan
            description: WAN
            iface: vtnet1
            enabled: true
            lock: true
            address: "192.168.10.90"
            subnet: "24"
            gateway: WAN_GW
            block_private: false
            block_bogon: false

          - name: lan
            description: LAN
            iface: vtnet0
            enabled: true
            lock: true
            address: "192.168.69.1"
            subnet: "24"
```

License
-------

MIT

Author Information
------------------

A role developed by [Mircea-Pavel ANTON](https://www.mirceanton.com).
