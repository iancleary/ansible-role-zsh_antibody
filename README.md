ansible-role-zsh_antibody
=========

[![Build Status](https://travis-ci.com/iancleary/ansible-role-zsh_antibody.svg?branch=main)](https://travis-ci.com/iancleary/ansible-role-zsh_antibody)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-iancleary.zsh_antibody-blue.svg)](https://galaxy.ansible.com/iancleary/zsh_antibody)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/iancleary/ansible-role-zsh_antibody/main/LICENSE)

This role installs the [ZSH](https://www.zsh.org/), with the [antibody](https://getantibody.github.io/) plugin manager, onto a supported Linux system (see Requirements section below for list of supported OS).

Plugins can be found here:

* <https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins>
* <https://github.com/zsh-users> (only select repos are plugins)

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here.

Supported and Tested `ansible_os_families`:

* Ubuntu 18.04
* Ubuntu 20.04
* Fedora 31
* Fedora 32

> Pull Requests welcome!

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

```yaml
---
antibody_version: "6.0.1"
antibody_bundles:
  # Bundles from the default repo (robbyrussell's oh-my-zsh) only need a name
  # https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins
  #
  # `name` is required (any valid file name will do so long as it's unique for the bundles)
  # `repo` is git username
  # `repo
  # `version` is git release and is required if `url` is defined
  - name: gitfast
  # - name: pipenv
  - name: poetry
  - name: yarn
  - name: zsh
  # Syntax highlighting bundle.
  - name: zsh-syntax-highlighting
    git:
      user: zsh-users
      repo: zsh-syntax-highlighting
      version: 0.7.1
  # Autosuggestions
  - name: zsh-autosuggestions # `name` is required (any valid file name will do so long as it's unique for the bundles)
    git:
      user: zsh-users
      repo: zsh-autosuggestions
      version: v0.6.4
  # ZSH Theme
  - name: powerlevel10k
    git:
      user: romkatv
      repo: powerlevel10k
      version: v1.12.0
zsh_theme: robbyrussell
zsh_custom_shell_command: "false"
# useful when users are bound to external systems (i.e. active directory)
# zsh_custom_shell_command: "true"
# zsh_default_shell_command: "/opt/pbis/bin/config LoginShellTemplate /usr/bin/zsh"
```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  roles:
    - role: iancleary.zsh_antibody
      users:
        - username: test_usr1
        - username: test_usr2
        - username: test_usr3
          skip_zshrc: true
      antibody_bundles:
        - name: gitfast
        - name: poetry
        - name: yarn
        - name: zsh
        # Syntax highlighting bundle.
        - name: zsh-syntax-highlighting
          repo:
            user: zsh-users
            repo: zsh-syntax-highlighting
            version: 0.7.1
```

> Note: the role currently assumes:

* all users want the same plugins, pull requests welcome if you'd prefer per user `antibody_bundles`

License
-------

[MIT](LICENSE)

Author Information
------------------

This role was created in 2020 by [Ian Cleary](https://iancleary.me).

It was derived from the MIT licensed [gantsign/ansible-role-oh-my-zsh](https://github.com/gantsign/ansible-role-oh-my-zsh) and [gantsign/ansible-role-antigen](https://github.com/gantsign/ansible-role-antigen).

> I prefer to use antibody, so if you prefer antigen, please use the above antigen repo!

Inspiration for the structure of this repo came from [Jeff Geerling](https://github.com/geerlingguy/ansible-role-nginx).
