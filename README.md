# Ansible Playbooks

A collection of minimalist Ansible playbooks for automating server setups.

- [Initial ansible setup](./setup_ansible): this playbook will prepare your ansible environnements
- [Update system packages](./update_packages/): this playbook will update RHEL & Debian family Linux distros. Additionnal packages can be also installed.
- [Install Docker CE](./setup_docker/): this playbook install docker-ce
- [Install Docker Swarm](./setup_dockerswarm/): this playbook configure a docker swarm cluster
- [Install GlusterFS](./setup_glusterfs/): this playbook install and configure a glusterfs cluster (distributed file system)

# Inventory

```
[manager]
docker01

[workers]
docker02
docker03
```

# Run-it

```
ansible-playbook setup_ansible/playbook.yml --ask-pass -u root
ansible-playbook update_packages/playbook.yml
ansible-playbook setup_docker/playbook.yml
ansible-playbook setup_dockerswarm/playbook.yml
ansible-playbook setup_glusterfs/playbook.yml
```