# Ansible Role: ansible-common

[![Build Status](https://travis-ci.org/coglinev3/ansible-common.svg?branch=master)](https://travis-ci.org/coglinev3/ansible-common)

Setup defaults (Ansible module dependencies, software packages) for every supported Linux distribution:
* Alpine Linux 3.9,
* Debian 8 (Jessie),
* Debian 9 (Stretch),
* Debian 10 (Buster),
* Enterprise Linux 6, 
* Enterprise Linux 7, 
* Ubuntu 14.04 LTS (Trusty Tahr),
* Ubuntu 16.04 LTS (Xenial Xerus),
* Ubuntu 17.10 (Artful Aardvark),
* Ubuntu 18.04 LTS (Bionic Beaver) and
* Ubuntu 18.10 (Cosmic Cuttlefish).

This role is designed to run on every system as a initial setup. On the one
hand, essential packages for Ansible modules and, on the other hand, standard
packages for each Linux system are installed. Since each system administrator
uses other Ansible modules, they can be defined using the `essential_packages`
variable itself. The same applies to the standard packages. Because each system
administrator or company has its own preferences for the packages to install on
each system, those packages can be specified with the variable `common_packages`.

The role was tested with Docker on Travis-CI and with this [Multi-VM Vagrant environment](https://ansible-development.readthedocs.io/ "Vagrant environment for Developing and Testing Ansible Roles").

## Requirements

* On Ubuntu servers, the python-minimal package must be installed before you can
execute this role.
* On Alpine Linux servers, the Python package must be installed before you can
execute this role.

## Role Variables

Available variables are listed below, along with default values
(see defaults/main.yml):

```yml
# Essential packages for some ansible modules. The defaults provided by this
# role are specific to each distribution.

essential_packages:
  - bzip2
  - git
  - python-apt
  - python-httplib2
  - python-jinja2
  - python-lxml
  - python-selinux
  - python-semanage
  - python-yaml
  - rsync
  - unzip
  - zip

# Standard packages for every system. The defaults provided by this role are
# specific to each distribution. You can define your own packages for example
# over a group_var or host_var definition.

common_packages:
  - curl
  - htop
  - net-tools
  - psmisc
  - vim
  - vim-common

# default package states: present | latest | absent
essential_packages_state: present
common_packages_state: present
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
    - { role: coglinev3.ansible-common }
```

Using a pre_tasks statement on Ubuntu systems can ensure that the python-minimal
package is installed. Thanks for discussion on [gist.github.com](https://gist.github.com/gwillem/4ba393dceb55e5ae276a87300f6b8e6f "gwillem/ansible-bootstrap-ubuntu-16.04.yml")

```yml
---
- hosts: ubuntu-nodes
  gather_facts: False
  become: true
  # This will install python2 if missing on ubuntu (but checks first so no
  # expensive repeated apt updates)
  pre_tasks:
    - name: Install python for Ansible
      raw: test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
      register: output
      changed_when: output.stdout != ""
    - setup: # aka gather_facts

- hosts: all
  become: true
  roles:
    - { role: coglinev3.ansible-common }
```

## Version

Release: 1.1.1

## License

BSD

## Author Information

This Ansible Role was created in 2018, by Cogline.v3.
