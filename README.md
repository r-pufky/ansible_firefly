# Firefly
Firefly installation from public release tarball.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_firefly/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_firefly/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_firefly/blob/main/defaults/main/ports.yml)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.srv](https://github.com/r-pufky/ansible_collection_srv) collection.

## Example Playbook
Read defaults documentation.

Install Firefly using sqlite and redis caching. Version (and databases) will be
migrated and updated on new releases.

``` yaml
- name: 'firefly server'
  hosts: 'firefly.example.com'
  become: true
  roles:
     - 'r_pufky.srv.firefly'
  vars:
    firefly_cfg_auth_static_cron_token: '{CRON TOKEN}'
    firefly_cfg_db_app_key: '{DB_APP_KEY}'
```

Alternative setup using memcached, postgres, and enabling weekly storage
backups.

``` yaml
- name: 'firefly server'
  hosts: 'firefly.example.com'
  become: true
  roles:
     - 'r_pufky.srv.firefly'
  vars:
    firefly_srv_redis_enable: false
    firefly_srv_memcached_enable: true
    firefly_cfg_app_session_driver: 'memcached'
    firefly_cfg_app_cache_driver: 'memcached'
    firefly_cfg_db_connection: 'pgsql'
    firefly_cfg_db_host: '192.168.0.10'
    firefly_cfg_db_port: 5432
    firefly_cfg_db_database: 'firefly'
    firefly_cfg_db_username: 'firefly'
    firefly_cfg_db_password: '{PASSWORD}'
    firefly_srv_backup_dir: '/data/firefly/backup'
    firefly_srv_backup_enable: true
    firefly_srv_backup_schedule: 'weekly'
    firefly_cfg_auth_static_cron_token: '{CRON TOKEN}'
    firefly_cfg_db_app_key: '{DB_APP_KEY}'
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_srv/blob/main/docs/dev/environment/README.md)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-2.0.3-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_firefly)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_firefly/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_firefly/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
