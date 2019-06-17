# Config os-profiler in Overcloud with ansible
## Introduction
This document details using Ansible to config deployed overcloud enable os-profiler.
More information about os-profiler follow this [link](https://docs.openstack.org/osprofiler/latest/)
## Configuration recommand
The following minimum configuration is recommended.
```
[defaults]
retry_files_enabled = False
log_path = ansible.log
forks = 25
timeout = 30
gather_timeout = 30
remote_user = heat-admin

[inventory]

[privilege_escalation]

[paramiko_connection]

[ssh_connection]
ssh_args = -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -o ControlMaster=auto -o ControlPersist=30m -o ServerAliveInterval=5 -o ServerAliveCountMax=5
pipelining = True
```
## How to use
1. Generate inventory file with overcloud tool.
```
tripleo-ansible-inventory --ansible_ssh_user heat-admin \
                          --config-file ansible.cfg \
                          --static-yaml-inventory inventory.yaml\
                          --plan rockycloud                          
```
2. Edit variable file `vars/roles.yaml` for overcloud role.
3. Generate playbook
```
ansible-playbook generate-playbook.yaml
```
4. Config os-profiler
```
bash config-os-profiler.sh
```
## Advance usage
## Limitation
* This playbook only works when overcloud deployed.
