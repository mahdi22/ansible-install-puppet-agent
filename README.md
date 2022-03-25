![Ansible](https://img.shields.io/ansible/role/d/51467)
![Ansible](https://img.shields.io/ansible/quality/51467)
[![Galaxy](https://img.shields.io/ansible/role/51467)](https://galaxy.ansible.com/mahdi22/puppet_agent)
# Ansible role `puppet_agent`


An Ansible role for installing agent puppet (supported version 6 and 7 if install agent from puppetlabs repository, else all version is supported) in RHEL/CentOS, Debian and Ubunut distributions. Specifically, the responsibilities of this role are to:

- Install puppet from official repositories
- Configuration puppet agent
- Generate certification
- Enable puppet service
- Start puppet service

## Installation
``` bash
$ ansible-galaxy install mahdi22.puppet_agent
```

## Role Variables

This role has multiple variables. The defaults for all these variables are the following:

```yaml
---
# Specify if the role must use a proxy web
# Default is False
use_proxy: yes

# If use_proxy: yes, set http proxy variables environment
# Replace proxy.local with your web proxy adresse or name
# Replace 8080 with your web proxy port
proxy_env:
  http_proxy: http://proxy.local:8080/
  https_proxy: http://proxy.local:8080/

# Set install_from_puppetlabs: True - install puppet agent from puppetlabs repository.
# Set install_from_puppetlabs: False - do not install puppetlabs repositry
# Default is true.
install_from_puppetlabs: True

# Specifie puppet version
# Supported values are "6" and "7"
# This parameter is valid if install_from_puppetlabs: True
# Default is 6
puppet_version: "6"

# Generate or Re-generate a new certificat
# Turne this variable to false to edit configuration without generate a new certificat
# Default is True
puppet_agent_certification: True

# The master server to request configurations from.
# Defaults to puppet
puppet_server_name: puppet.lab

# The environment to request when contacting the master.
# Default is production
environment: production

# How often to do a Puppet run, when running as a service.
# Default is 30m
runinterval: 30m
```

## Dependencies

None

## Example Playbook

Playbook example to execute role without proxy web
```Yaml
- hosts: puppet
  roles:
    - role: mahdi22.puppet_agent
      become: yes
      vars:
        puppet_server_name: puppet.lab
        puppet_version: "7"
```
Playbook example to execute role with proxy web
```Yaml
- hosts: puppet
  roles:
    - role: mahdi22.puppet_agent
      become: yes
      vars:
        puppet_server_name: puppet.lab
        puppet_version: "7"
        use_proxy: yes
        proxy_env:
          http_proxy: http://proxy.local:8080/
          https_proxy: http://proxy.local:8080/
```

Playbook example to execute role with proxy web and without using puppetlabs repository 
```Yaml
- hosts: puppet
  roles:
    - role: mahdi22.puppet_agent
      become: yes
      vars:
        puppet_server_name: puppet
        use_proxy: yes
        proxy_env:
          http_proxy: http://proxy.local:8080/
          https_proxy: http://proxy.local:8080/
        install_from_puppetlabs: False
```
## Testing

This role is tested on Linux distributions:

- RHEL/CentOS 8
- RHEL/CentOS 7
- Debian 10
- Debian 9
- Debian 8
- Ubuntu 20.04
- Ubuntu 18.04
- Ubuntu 16.04
