# Ansible Role: ansible-common

[![Build Status](https://travis-ci.org/coglinev3/ansible-common.svg?branch=master)](https://travis-ci.org/coglinev3/ansible-common)

Setup defaults (Ansible module dependencies, software packages, bash dotfiles, etc.) for every supported Linux distribution:
* Enterprise Linux 6, 
* Enterprise Linux 7, 
* Ubuntu 16.04 LTS (Xenial Xerus),
* Ubuntu 17.10 (Artful Aardvark),
* Debian 8 (Jessie) and
* Debian 9 (Stretch).

This role is designed to run on every system as a initial setup. On the one hand, essential packages for Ansible modules and, on the other hand, standard packages for each Linux system are installed. Since each system administrator uses other Ansible modules, they can be defined using the essential_packages variable itself. The same applies to the standard packages. Because each system administrator or company defines its own preferences for the packages to install on each system, they can be specified using the common_packages variable.

## Requirements

On Ubuntu servers, the python-minimal package must be installed for Ansible to work.

## Role Variables

Available variables are listed below, along with default values:

```yml
# Essential packages for some ansible modules. The defaults provided by this
# role are specific to each distribution.

# essential_packages:
#  - python-apt
#  - python-selinux
#  - python-semanage
#  - python-lxml
#  - git
#  - unzip


# Standard packages for every system. The defaults provided by this role are
# specific to each distribution. You can define your own packages for example
# over a group_var or host_var definition.

# standard_packages:
#  - net-tools
#  - psmisc
#  - vim
#  - curl
```

## Dependencies

None.

## Example Playbook

```yml
---
# file: roles/ansible-common/tests/test.yml

- hosts: all
  become: true
  roles:
    - { role: ansible-common }
```

## Version

Release: x.y.z

## License

BSD

## Author Information

This Ansible Role was created in 2018, by Cogline.v3.
