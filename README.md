# ansible-role-antigen
An ansible role to install [zsh-users/antigen](https://github.com/zsh-users/antigen).

installation
============

The preferred way to install this role is through ansible-galaxy.

    ansible-galaxy install nifr.antigen

Usage
=====

After installation you can use antigen in your `~/.zshrc` (local) or `/etc/zsh/zshrc` (global).

Example .zshrc:

    # Add antigen's path to the "fpath" array (which corresponds to $FPATH)
    fpath=("$HOME/.local/share/zsh/functions" $fpath)

    # Load antigen from zsh's function path. 
    # -U causes alias expansion to be suppressed when the function is loaded.
    # -z flags makes the function be loaded using zsh-style autoloading
    autoload -Uz antigen

    # This is a shortcut for "antigen bundle robbyrussell/oh-my-zsh"
    antigen use oh-my-zsh

    # Load a single plugin with the "antigen bundle" command
    antigen bundle zsh-users/zsh-syntax-highlighting

    # Load multiple plugins at once
    antigen bundles <<EOBUNDLES

      # This plugin adds many completions that are not included by default.
      zsh-users/zsh-completions

      # An intelligent helper that will replace the current (or previous) command line 
      # with the command you will want to run next. Press Ctrl+U to activate.
      oknowton/zsh-dwim

      # A very minimal prompt that includes git status information and little more.
      sindresorhus/pure

    EOBUNDLES


Defaults
=========

    antigen_install_global: false
    antigen_file_owner:     ~
    antigen_file_path:      ~{{ antigen_file_owner }}/.local/share/antigen/antigen.zsh
    antigen_file_group:     {{ antigen_file_owner }}
    antigen_file_mode:      0700
    antigen_download_url:   https://raw.githubusercontent.com/zsh-users/antigen/master/antigen.zsh
    antigen_download_force: false

Variables
=========

**antigen_install_global** (bool)

This setting configures wether to install antigen into a user's $HOME directory or globally for all users.
It defaults to a local installation. 

    true =>
       antigen_file_owner: {{ remote_user }}
       antigen_file_path:  ~{{ remote_user }}/.local/share/zsh/functions/antigen
       antigen_file_mode:  0700

    false =>
       antigen_file_owner: root
       antigen_file_path:  /usr/share/zsh/functions/antigen
       antigen_file_mode: 0755


**antigen_file_path** (string:file-path)

The target path where antigen should be downloaded to.

Defaults to:
* `%HOME%/.local/share/antigen/antigen.zsh` for local installation
* `/usr/share/antigen/antigen.zsh` for global installation

**antigen_file_owner** (string:username)

The user for which antigen should be installed.
This defaults to the ansible's SSH user on the remote machine.

**antigen_file_mode** (string:file-mode)

The file-mode passed to CHMOD - defaults to 0700 and 0755 if the username is 'root'.

**antigen_download_url** (string:url)

The URL where antigen should be downloaded from.

**antigen_download_force** (bool)

This setting configures wether antigen should be downloaded even if the file already exists.

License
=======
[MIT](https://github.com/nifr/ansible-role-antigen/LICENSE)

