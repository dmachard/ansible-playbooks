This playbook will execute a initial ansible setup.
Must be executed with root user on remote hosts.

The following steps are executed:
- add automation user for ansible
- push the public key of your ansible server
- disable root login
- disable ssh password authentication
- restart ssh

Vars:

- create_user: name of the user for ansible