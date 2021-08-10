Role Name
=========

Kodo Endpoints is a backup solution for Windows and MacOS desktops and laptops supporting Continous Data Protection
mechanism (CDP). This role deploys Kodo Endpoints Server which is a central point of management.

Requirements
------------

CentOS Stream/RHEL 8 minimal installation and public key authentication between command host and target machine

Role Variables
--------------

Defaults:
```
mariadb_version: "10.4"
mariadb_distro: "centos{{ ansible_distribution_major_version }}-amd64"
mariadb_repo_url: "http://yum.mariadb.org/{{ mariadb_version }}/{{ mariadb_distro }}"
mariadb_repo_gpg_key: "https://yum.mariadb.org/RPM-GPG-KEY-MariaDB"
kodo_repo: "http://repo.storware.eu/kodo-endpoints/current"
kodo_staging_path: "/kodo_data"
```

* `mariadb_*` - responsible for MariaDB installation (repository, version, distribution)
* `kodo_repo` - points to Kodo Endpoints RPM repository
* `kodo_staging_path` - allows to configure where staging space resides on the server
* `kodo_backup_destination_path` - allows to configure where backup storage resides on the server


Dependencies
------------

N/A

Example Playbook
----------------

This deploys Kodo server on `server` host (only one server can be deployed)
and multiple agents on `agents` hosts

```
- hosts: server
  roles:
   - xe0nic.ansible_kodo_endpoints_server
```

Example hosts inventory (you need to make sure that SSH public key authentication for
ansible user provided in inventory is configured):

```
[all:vars]
ansible_user = root

[server]
192.168.155.233
```

License
-------

MIT

Author Information
------------------

For more information visit product website: https://storware.eu/products/kodo-for-endpoints
Documentation: https://storware.gitbook.io/kodo-for-endpoints