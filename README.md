# [Ansible role testing](#testing)

Ping Ping Testing

|GitHub|GitLab|Downloads|Version|Issues|Pull Requests|
|------|------|-------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-testing/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-testing/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-testing/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-testing)|[![downloads](https://img.shields.io/ansible/role/d/4856)](https://galaxy.ansible.com/buluma/testing)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-testing.svg)](https://github.com/buluma/ansible-role-testing/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-testing.svg)](https://github.com/buluma/ansible-role-testing/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-testing.svg)](https://github.com/buluma/ansible-role-testing/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-testing/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    # - role: buluma.systemd
    # # - name: buluma.python_pip
    # - role: buluma.sysctl
    - role: buluma.testing
      facts:
        - key: datacenter
          value: Nairobi
        - key: availability_zone
          value: west
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-testing/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no
  vars:
    python_pip_executable: pip3
    python_pip_update: yes
    default_unit_state: "stopped"
    default_unit_type: "service"
    default_unit_enabled: "yes"
    default_systemd_backup_files: true

  roles:
    - name: buluma.bootstrap
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-testing/blob/master/defaults/main.yml):

```yaml
---
# defaults file for ansible-role-testing
# Do you want to wait for the host to be available?
sudo_wait_for_host: no

# The number of seconds you want to wait during connection test before failing.
sudo_timeout: 3

powertools_repo_path: "/etc/yum.repos.d/{{ _powertools_repo_file[ansible_distribution] }}"

forensics_command_list:
  - "journalctl -xe"
  - "ps -ef"
  - "lsof"
  - "systemctl status"
  - "netstat -an"
  - "netstat -tulpen"

# A directory where collected data can be stored locally.
forensics_local_storage_path: /tmp/forensics

# A list of directories to collect all files from.
forensics_directory_list:
  - "/var/log"
  - "/tmp"
  - "/var/tmp"
  - "/var/spool/cron"
  - "/var/spool/anacron"
  - "/etc/cron.d"
  - "/etc/cron.daily"
  - "/etc/cron.hourly"
  - "/etc/cron.monthly"
  - "/etc/cron.weekly"
  - "/var/spool/at"

# A list of files to collect.
forensics_file_list:
  - "/etc/passwd"
  - "/etc/group"
  - "/etc/shadow"

# A list of directories and patterns to collect.
forensics_specific_file_list:
  - path: "/root"
    pattern: ".authorized_keys"
  - path: "/root"
    pattern: ".bash_history"
  - path: "/root"
    pattern: ".history"
  - path: "/home"
    pattern: ".authorized_keys"
  - path: "/home"
    pattern: ".bash_history"
  - path: "/home"
    pattern: ".history"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-testing/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Build Status GitHub](https://github.com/buluma/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-buildtools/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-buildtools)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.systemd](https://galaxy.ansible.com/buluma/systemd)|[![Build Status GitHub](https://github.com/buluma/ansible-role-systemd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-systemd/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-systemd/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-systemd)|
|[buluma.python_pip](https://galaxy.ansible.com/buluma/python_pip)|[![Build Status GitHub](https://github.com/buluma/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-python_pip/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-python_pip)|
|[buluma.sysctl](https://galaxy.ansible.com/buluma/sysctl)|[![Build Status GitHub](https://github.com/buluma/ansible-role-sysctl/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-sysctl/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-sysctl/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-sysctl)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-testing/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-testing/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-testing/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-testing/blob/master/LICENSE).

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)

Please consider [sponsoring me](https://github.com/sponsors/buluma).

### [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
