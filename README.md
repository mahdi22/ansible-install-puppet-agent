# Ansible role `mariadb_install`


An Ansible role for installing and secure agent puppet version 6 in RHEL/CentOS (6,7,8) and Debian (9,10) and Ubunut (20.04, 18.04, 16.04) distributions. Specifically, the responsibilities of this role are to:

- Install puppet 6 official repositories
- Configuration puppet agent
- Generate sertification
- Enable puppet service
- Start puppet service

## Installation
``` bash
$ ansible-galaxy install mahdi22.puppet_agent
```

## Role Variables

### Basic configuration

| Variable                       | Default                       | Comments                                                     |
| :---                           | :---                          | :---                                                         |
| `http_proxy     `              | 'http://proxy.lab.local:8080/'| Set Proxy server and port replace proxy.lab.local:8080       |
| `https_proxy`                  | 'http://proxy.lab.local:8080/'| Set Proxy server and port replace proxy.lab.local:8080       |
| `puppet_server_name`           | puppetserver.lab.local        | Set the puppet server name or ip address                     |
| `environnement`                | production                    | set the puppet environement.                                 |
| `runinterval`                  | 3306                          | Set puppet run interval                                      |

#### Remarks

(1) Remove the folowing parameters on all install packages tasks if machines have an internet access without proxy server .:
```yaml
environment: "{{ proxy_env }}"
```

## Example Playbook

```Yaml
- hosts: puppet
  roles:
    - role: mahdi22.puppet_agent
      become: yes
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