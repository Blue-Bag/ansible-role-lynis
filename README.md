Ansible Role: Lynis
=========

[![Build Status](https://travis-ci.org/Blue-Bag/ansible-role-lynis.svg?branch=master)](https://travis-ci.org/Blue-Bag/ansible-role-lynis)

Installs the [Lynis](https://cisofy.com/lynis/) security auditing tool on RHEL/CentOS or Debian/Ubuntu servers.

Updated to add the Cisofy repo as package soure as the APT packages are too out of date.

Requirements
------------

None.

Role Variables
--------------

```yml
lynis_version: 3.0.8
lynis_version_sha256sum: 98373a4cc9d0471ab9bebb249e442fcf94b6bf6d4e9c6fc0b22bca1506646c63
```
The version and corresponding `sha256sum` of Lynis to install. Latest version and hash can be found on the [Lynis download page](https://cisofy.com/download/lynis/).

```yml
lynis_src_directory: /usr/local/src/
```
The directory to store the `.tar.gz` and Lynis src files.

```yml
lynis_dest_directory: /opt
```
The directory to hold the Lynis installation.

```yml
lynis_log_directory: /var/log/lynis
```
The directory for the Lynis logs. Used by the cron job. By default Lynis will output the report to `stdout` and log to `/var/log/lynis.log` and `/var/log/lynis-report.dat`.

```yml
lynis_cron: yes
lynis_cron_weekday: "*"
lynis_cron_hour: 3
lynis_cron_minute: 30
```
Lynis cron job configuration. The report, report log, and report data are all written to the `lynis_log_directory`.

Custom Configuration
```yml
lynis_custom_cfg: yes
lynis_custom_cfg_path: 'templates/custom.prf.j2'
```
This enables you to overide the default configuration.
the out of the box config overides the certficate path for checkingcertificates.
This stops Lynis reporting on archived certificates for LetsEncrypt.
Youcan reference you own custom file if you have additional config to override.

Dependencies
------------

None.

Example Playbook
----------------

```yml
- hosts: all
  roles:
     - { role: ansible-role-lynis, tags: [lynis] }
```

License
-------

MIT / BSD
