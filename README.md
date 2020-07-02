# aviAzureBootstrap

## Goals
Bootstrap Avi cntroller (Through Ansible playbooks) in Azure

## Prerequisites:
1. Make sure Ansible in installed in the orchestrator VM
2. Make sure avisdk is installed:
```
pip install avisdk
ansible-galaxy install -f avinetworks.avisdk
```

## Environment:
Playbook(s) has/have been tested against:

### Ansible

```
avi@ansible:~/ansible/aviSlackAlerts$ ansible --version
ansible 2.9.5
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/avi/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /home/avi/.local/lib/python2.7/site-packages/ansible
  executable location = /home/avi/.local/bin/ansible
  python version = 2.7.12 (default, Oct  8 2019, 14:14:10) [GCC 5.4.0 20160609]
avi@ansible:~/ansible/aviSlackAlerts$
```

### Avi version

```
Avi 18.2.8
```

## Input/Parameters:

- All the paramaters/variables are stored in var/params.yml.
```
aviPassword: Avi_2020
```

- An ansible host (hosts) file is required:
```
---
all:
  children:
    jump:
      hosts:
        172.16.1.4:
    controller:
      hosts:
        172.16.1.5:
    webA:
      hosts:
        172.16.2.4:
        172.16.2.5:
  vars:
    ansible_user: "avi"
    ansible_ssh_private_key_file: "/home/avi/.ssh/id_rsa.azure"
```

- A credential file (vars/creds.json)is required:
```
avi_cluster: false
avi_credentials:
  api_version: 18.2.8
  controller: 172.16.1.5
  username: admin
```

## Use the ansible playbook to:
1. Configure your password
2. Generate a json file with the new credentials

## Run the playbook:
ansible-playbook -i hosts main.yml

## Improvement:
