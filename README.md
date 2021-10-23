# Ansible Playbooks

A collection of minimalist Ansible playbooks for automating server setups.

- Initial ansible setup
- Update system packages
- Install Docker CE

```
ansible-playbook setup_ansible/playbook.yml --ask-pass -u root
ansible-playbook update_packages/playbook.yml
ansible-playbook setup_docker/playbook.yml
```