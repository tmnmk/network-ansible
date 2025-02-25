# This README describes how to run various ansible playbooks in this repo for network automation purposes

### Getting started
At that moment this Ansible repo contains two playbooks:
- change global settings on Cisco devices (__change_global_cisco.yaml__);
- create subinterfaces on Palo Alto devices (__create_interfaces_paloalto.yaml__).

## Playbook 1 - Change global setting on Cisco devices
If you want to change some global settings staff on Cisco devices you should run the playbook __change_global_cisco.yaml__.
You MUST run this playbook with *--tag* and *--limit* variabales. 
It uses ROLE *change_global_cisco* which contains some tasks. They described bellow, you may see tags:

    - log_settings
    - ntp_settings
    - snmp_settings
    - create_user

## Playbook 2 - Create subinterfaces on Palo Alto devices
If you want to create subinterfaces on Palo Alto devices you should run the playbook __create_interfaces_paloalto.yaml__.
You MUST run this playbook with *--tag* and *--limit* variabales. 
It uses ROLE *create_interfaces_paloalto* which contains some tasks. They described bellow, you may see tags:

    - interface_dhcp
    - interface

## Example of command:
- change NTP on Alpha cisco devices
```
ansible-playbook change_global_cisco.yaml --tags ntp_settings --limit access_sw_alfa --ask-vault-pass
```
- change log settings on Alpha cisco devices
```
ansible-playbook change_global_cisco.yaml --tags log_settings --limit access_sw_alfa --ask-vault-pass
```
- create subinterfaces on Alpha Palo Alto devices
```
ansible-playbook create_interfaces_paloalto.yaml --tags interface --limit alfa-edge-fw01 --ask-vault-pass
```


 
