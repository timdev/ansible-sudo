# Ansible Sudo Role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-sudo.svg)](https://travis-ci.org/weareinteractive/ansible-sudo)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.sudo-blue.svg)](https://galaxy.ansible.com/list#/roles/1380)
[![GitHub Tags](https://img.shields.io/github/tag/weareinteractive/ansible-sudo.svg)](https://github.com/weareinteractive/ansible-sudo)
[![GitHub Stars](https://img.shields.io/github/stars/weareinteractive/ansible-sudo.svg)](https://github.com/weareinteractive/ansible-sudo)

> `sudo` is an [ansible](http://www.ansible.com) role which:
>
> * installs sudo
> * configures sudo

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.sudo
```

Using `requirements.yml`:

```
- src: franklinkim.sudo
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-sudo.git franklinkim.sudo
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# sudo_users:
#  - { name: '%foo', nopasswd: yes, requiretty: no }
#  - { name: 'bar', nopasswd: no }
#  - name: '%foo'
#    nopasswd: yes
#    commands: '/bin/ls'
#  - name: 'bar'
#    nopasswd: no
#    commands: '/bin/nano'
#  - name: '%foo'
#    nopasswd: yes
#    commands: '/bin/nano /etc/hosts'
#  - name: 'baz'
#    nopasswd: yes
#    requiretty: no


# list of username or %groupname
sudo_users: []

# Default require tty option 
# It should be overriden with vars in your playbook based on the actual distribution
#
# - hosts: all
#    tasks:
#    - include_vars: "os_{{ ansible_distribution }}.yml"
#
# It can also be passed explicitely to the role
#
# roles:
#  - role: franklinkim.sudo
#    default_requiretty: true
#    sudo_users:
#      - name: '%sudo'
#        nopasswd: yes
#        requiretty: no
#
default_requiretty: false
```


## Example playbook

```
- host: all
  sudo: yes
  roles:
    - franklinkim.sudo
  vars:
    default_requiretty: no
    sudo_users:
      - { name: 'foo', nopasswd: no, requiretty: yes }
      - { name: '%sudo', nopasswd: yes }
      - name: '%foo'
        nopasswd: yes
        commands: '/bin/ls'
      - name: 'bar'
        nopasswd: no
        commands: '/bin/nano'
      - name: '%foo'
        nopasswd: yes
        commands: '/bin/nano /etc/hosts'
      - name: 'baz'
        nopasswd: yes
        requiretty: yes
```

## Testing

```
$ git clone https://github.com/weareinteractive/ansible-sudo.git
$ cd ansible-sudo
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) We Are Interactive under the MIT license.
