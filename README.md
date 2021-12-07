`dimmaryanto93.checkmk_agent`
=========

Repository ini digunakan untuk menginstall [checkmk_agent](https://docs.checkmk.com/latest/en/agent_linux.html) untuk Linux

Support platform

- Debian
- Ubuntu
- CentOS


Ansible - User Guide
------------

Persiapan yang harus di lalukan, diantaranya

1. Create new user on your server, Recomend using **very-very Strong Password** or using password generator. 
  ```bash
  adduser <username>
  ```

2. Granted to sudoers with NOPASSWD, using `visudo`
  ```ini
  username    ALL=(ALL) NOPASSWD:ALL
  ```

3. Authenticate with private-key for login ssh, generate ssh key on your local machine then use `ssh-copy-id user@your-ip-server` to copy public key to your server.


Requirements
------------

Untuk menggunakan role ini, kita membutuhkan package/collection 

- [ansible.posix](https://github.com/ansible-collections/ansible.posix)
- [community.general](https://github.com/ansible-collections/community.general)

Temen-temen bisa install, dengan cara 

```bash
ansible-galaxy collection install ansible.posix community.general
```

Atau temen-temen bisa menggunakan `requirement.yaml` file and install menggunakan `ansible-galaxy collection install -r requirement.yaml`, dengan format seperti berikut:

```yaml
---
collections:
  - ansible.posix
  - community.general
```

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting docker daemon, diantaranya seperti berikut:

| Variable name               | Example value                     | Description |
| :---                        | :---                              | :---        |
| `checkmk_server_url`        | `http://localhost:8080`           |             |
| `checkmk_agent_version`     | `2.0.0p6-1`                       |             |
| `checkmk_agent_only_from`   | `['localhost', '192.168.88.10']`  | Untuk memprotect data yang di expose oleh `check_mk_agent` yang boleh di access oleh ip tersebut |
| `checkmk_agent_port`        | `'6556'`                          | Port yang di gunakan untuk berkomunikasi dengan `checkmk_server` |

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  become: true
  roles:
      - { role: dimmaryanto93.checkmk_agent }
```

License
-------

MIT