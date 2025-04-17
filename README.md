# This README describes how to run various ansible playbooks in this repo for network automation purposes

### Getting started
This Ansible repo contains several playbooks for network device configuration:

1. **Change global settings on Cisco devices** (`change_global_cisco.yaml`)
2. **Create subinterfaces on Palo Alto devices** (`create_interfaces_paloalto.yaml`)
3. **Configure L2 interfaces on Cisco devices** (`configure_l2_interfaces_cisco.yaml`)
4. **Configure L2 interfaces on Huawei S5700 devices** (`configure_l2_interfaces_huawei.yaml`)

## Playbook 1 - Change global settings on Cisco devices
If you want to change some global settings on Cisco devices, run the playbook `change_global_cisco.yaml`.
You MUST run this playbook with `--tag` and `--limit` variables.
It uses ROLE `change_global_cisco` which contains the following tasks (tags):

    - log_settings
    - ntp_settings
    - snmp_settings
    - create_user

## Playbook 2 - Create subinterfaces on Palo Alto devices
If you want to create subinterfaces on Palo Alto devices, run the playbook `create_interfaces_paloalto.yaml`.
You MUST run this playbook with `--tag` and `--limit` variables.
It uses ROLE `create_interfaces_paloalto` which contains the following tasks (tags):

    - interface_dhcp
    - interface

## Playbook 3 - Configure L2 interfaces on Cisco devices
If you want to configure L2 interfaces on Cisco devices, run the playbook `configure_l2_interfaces_cisco.yaml`.
This playbook configures:
- Access interfaces with VLANs and voice VLANs
- Trunk interfaces
- Port security
- Spanning-tree settings
- Disabled interfaces (parking VLAN)

## Playbook 4 - Configure L2 interfaces on Huawei S5700 devices
If you want to configure L2 interfaces on Huawei S5700 devices, run the playbook `configure_l2_interfaces_huawei.yaml`.
This playbook configures:
- Access interfaces with VLANs and voice VLANs
- Trunk interfaces
- Port security
- Spanning-tree settings
- Disabled interfaces (parking VLAN)

## Examples of commands:

### Cisco Global Settings
- Change NTP on Alpha cisco devices:
```
ansible-playbook change_global_cisco.yaml --tags ntp_settings --limit access_sw_alfa --ask-vault-pass
```
- Change log settings on Alpha cisco devices:
```
ansible-playbook change_global_cisco.yaml --tags log_settings --limit access_sw_alfa --ask-vault-pass
```

### Palo Alto Interfaces
- Create subinterfaces on Alpha Palo Alto devices:
```
ansible-playbook create_interfaces_paloalto.yaml --tags interface --limit alfa-edge-fw01 --ask-vault-pass
```

### Cisco L2 Interfaces
- Configure L2 interfaces on Cisco devices:
```
ansible-playbook configure_l2_interfaces_cisco.yaml --limit cisco-sw01 --ask-vault-pass
```

### Huawei L2 Interfaces
- Configure L2 interfaces on Huawei S5700 devices:
```
ansible-playbook configure_l2_interfaces_huawei.yaml --limit huawei-sw01 --ask-vault-pass
```

## Required Variables
For L2 interface configuration playbooks, ensure your host/group vars contain:
- `enabled_interfaces`: List of interfaces to be enabled with VLAN configuration
- `disabled_interfaces`: List of interfaces to be disabled and placed in parking VLAN
- `trunk_interfaces`: List of trunk interfaces with allowed VLANs
- Optional variables:
  - `port_security`: Boolean to enable port security
  - `portfast_edge`: Boolean to enable spanning-tree edge port
  - `mac_value`: Maximum number of MAC addresses for port security


 
