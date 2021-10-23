# Ansible Playbooks

A collection of minimalist Ansible playbooks for automating server setups.

- Initial ansible setup
- Update system packages

ansible-playbook setup_ansible/playbook.yml --ask-pass -u root
ansible-playbook update_packages/playbook.yml