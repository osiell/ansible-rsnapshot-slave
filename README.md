# rsnapshot (slave)

Ansible role to install rsync and configure the system to be backed up by
the `rsnapshot-master` role.
For this purpose, this role creates a system user with sudo privileges on
the `rsync` program. The public SSH key is get from the master host (defined by
the `rsnapshot-master` role) and added to the user's authorized keys.

Minimum Ansible Version: 1.5

## Supported Platforms

* Debian
    - squeeze   (6)
    - wheezy    (7)
    - jessie    (8)
* Ubuntu
    - precise   (12.04)
    - trusty    (14.04)

## Variables

```yaml
rsnapshot_master_host: False    # Must be defined
rsnapshot_master_host_user:  "{{ ansible_ssh_user }}"
rsnapshot_master_ssh_key: id_rsa

# User used by the rsnapshot master to connect on the configured host
rsnapshot_slave_user: backupuser
```

## Example (Playbook)

```yaml
- name: Hosts to backup
  hosts: remote_host_1:remote_host_2
  sudo: yes
  roles:
    - rsnapshot-slave
  vars:
    - rsnapshot_master_host: backup_master
```

See the `rsnapshot-slave` role for details.
