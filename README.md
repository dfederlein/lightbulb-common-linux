lightbulb-common-linux
=========

Configures and secures a Red Hat Enterprise Linux 7 or CentOS 7 base node for use in an Ansible Lightbulb lab environment.

This role will:

* Ensure firewalld and libselinux-python is present (RHEL7 only)
* Ensure firewalld is started (RHEL7 only)
* Enables specific firewalls services (RHEL7 only)
* Configures sshd and sudoers
* Creates a group and user for the assigned student owner

Requirements
------------

This role has no special requirements.

Role Variables
--------------

* *username*: This *required* variable contains a string with the student username that will be using the node in their lab. This variable is typically elsewhere using `set_fact` while provisioning or as a host variable in more static environments.

* *ssh_port*: This variable is an integer that defines the port the sshd service will be bound. It defaults to 22. Typically you will not want to change this. If you run on a port other than the default, remember you may also need to open that port in your firewalld service (RHEL7 only) and any VPC settings for SSH access to be possible.

* *admin_password*: This variable is a string defines the password for the `username` account on the node. It is recommended, but not required, you set this with a sufficiently unique password that all nodes in the lab can share. If unset one will be assigned password made up of "CowSay" and the month and year i.e. "CowSay1018".

* *firewalld_rules*: This variable contains a list of dictionaries that define the rules the firewalld service will be configured. Each dictionary in the list can contain a "service" name such as "http" or a "port" number and "protocol". See `defaults/main.yml` for an example definition.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
---
- hosts: nodes
  vars:
    username: lightbulb
    admin_password: ChAnGEthIs
  roles:
    - lightbulb-common-linux
```

License
-------

MIT

Author Information
------------------

This role has been developed as part of the [Ansible Lightbulb project](https://github.com/ansible/lightbulb).
