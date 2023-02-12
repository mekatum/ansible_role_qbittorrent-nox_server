# Ansible role for deploy self-hosted qBittorrent-nox server.

This Ansible role deploy and config self-hosted qBittorrent-nox server
on Alpine Linux.

## System requirements

So to run the playbook you will need:
* Ansible 2.12 on management node
 * Collections [community-general](https://github.com/ansible-collections/community.general)
* Alpine Linux >= 3.17 and python3 on managed node

## How to use it

Create the playbook `torrent.yaml` like below and override some variables

```yaml
- hosts: torrent.your-domain.local
  roles:
    - torrent
  become: True
  become_method: su
  vars:
    - alpine_version: 'v3.17'
    - alpine_repo_mirror: 'https://mirror.yandex.ru/mirrors/alpine'
```

And run this playbook with `ansible-playbook`
```console
user@host:~$ ansible-playbook torrent.yaml
```

## WebUI on ports 80/443

You can set any port for WebUI in the qBittorrent settings. But if port number
is less than 1024, you will need to set capabilities for the qBittorrent binary 
([binding to priveleged ports](https://man7.org/linux/man-pages/man7/capabilities.7.html)).

Change the port number in the playbook in accordance with the one you specified
in the WebUI settings and ansible will install the necessary capabilites.

***Important***: _changing port in the playbook does not change 
port for WebUI. To change port for WebUI, change it in 
the settings or in config file (by default 
in ```/var/lib/qbittorrent/.config/qBittorrent/qBittorrent.conf```)._

