# ansible-role-antigen
An ansible role to install [zsh-users/antigen](https://github.com/zsh-users/antigen).

installation
============

The preferred way to install this role is through ansible-galaxy.

    ansible-galaxy install nifr.antigen

defaults
=========

antigen:
  install:
    user:   ~
    global: false
  path: $HOME/.local/share/antigen/antigen.zsh
  url:
      https://raw.githubusercontent.com/zsh-users/antigen/master/antigen.zsh

variables
=========

**antigen.install.global**
*(string|path)*
Defaults to:
* `%HOME%/.local/share/antigen/antigen.zsh` for local installation
* `/usr/share/antigen/antigen.zsh` for global installation

**antigen.install.user**
*(string|username)*
The user for which antigen should be installed.
This defaults to the ansible's SSH user on the remote machine.

**antigen.path**
*(string|file-path)*
The target path where antigen should be downloaded to.

**antigen.url**
*(string|url)*
The URL where antigen should be downloaded.


license
=======
[MIT](https://github.com/nifr/ansible-role-antigen/LICENSE)

