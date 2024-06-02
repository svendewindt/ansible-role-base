Ansible role base
=========

This is an Ansible role to set some basic settings for my RHEL derivative-based machines.

Some settings are:

- Creating users and groups
- Managing packages
- Setting the timezone
- Setting some Git settings

Requirements
------------

There are no specific requirements for this role.

Role Variables
--------------

Below an overview of the variables for this role.

| variable                     | default                | explanation                                    |
| ---                          | ---                    | ---                                            |
| add_users                    | [ ]                    | users to add, see below for an example         |
| time_zone                    | Europe/Brussels        | set the timezon                                |
| selinux_state                | enforcing              | sets selinux to enforcing                      |
| selinux_booleans             | [ ]                    | manages sebooleans                             |
| firewall_allow_services      | [dhcpv6-client, ssh]   | allows services through firewall               |
| firewall_allow_ports         | [ ]                    | allows ports through firewall                  |
| firewall_disallow_services   | [cockpit]              | blocks services through firewall               |
| ssh_PasswordAuthentication   | "no"                   | whether to allow SSH password authentication   |
| ssh_PermitRootLogin          | "no"                   | whether to allow SSH root logins               |
| ssh_PermitEmptyPasswords     | "no"                   | wheter to permit empty SSH passwords           |
| git_user_name                | ""                     | set git_user_name in ~/.gitconfig              |
| git_user_email               | ""                     | set git_user_email in ~/.gitconfig             |
| git_push_default             | "simple"               | set git_push_default in ~/.gitconfig           |
| git_pull_rebase              | "true"                 | set git_pull_rebase in ~/.gitconfig            |
| git_core_autocrlf            | "input"                | set git_core_autocrlf in ~/.gitconfig          |


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

An example can be found in the /tests/test.yml.

```yml
---
- hosts: localhost
  remote_user: root

  vars:
    # Install
    install_packages: ["mlocate", "cockpit", "tar", "tmux", "bash-completion"]
    
    # Users
    add_users: 
      - name: sven
        comment: 'Sven de Windt'
        groups:
          - wheel
        # To create a password hash: mkpasswd -m sha-512  
        password: $6$Wpu1.R85...
        ssh_key: ssh-ed25519 AAAAC3Nz..

    # Config
    time_zone: "Europe/Brussels"
    selinux_state: enforcing
    selinux_booleans: []
    firewall_allow_services: [dhcpv6-client, ssh]
    firewall_allow_ports: []
    firewall_disallow_services: [cockpit] # use ssh portforwarding to access cockpit
    ssh_PasswordAuthentication: "no"
    ssh_PermitRootLogin: "no"
    ssh_PermitEmptyPasswords: "no"

    # Git
    git_user_name: "Github username"
    git_user_email: "Github email address"
    git_push_default: "simple"
    git_pull_rebase: "true"
    git_core_autocrlf: "input"

  roles:
    - ansible_role_base
```

License
-------

MIT

Author Information
------------------

This role is mainly created for myself, but I'm open for feedback and input.
