# Ansible Playbooks

A collection of minimalist Ansible playbooks for automating server setups.

- [Initial ansible setup](./setup_ansible): this playbook will prepare your ansible environnements
- [Update system packages](./update_packages/): this playbook will update RHEL & Debian family Linux distros. Additionnal packages can be also installed.
- [Install Docker CE](./setup_docker/): this playbook install docker-ce
- [Install Docker Swarm](./setup_dockerswarm/): this playbook configure a docker swarm cluster
- [Install GlusterFS](./setup_glusterfs/): this playbook install and configure a glusterfs cluster (distributed file system)
- [Install Terraform](./setup_terraform/): this playbook install terraform

# Inventory

$ cat /etc/hosts

```bash
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.1.220	ansible

192.168.1.221	docker-manager01
192.168.1.222	docker-worker01
192.168.1.223	docker-worker02
```

$ cat inventory.ini

```
[automation]
ansible

[swarm_managers]
docker-manager01

[swarm_workers]
docker-worker01
docker-worker02

[swarm:children]
swarm_managers
swarm_workers

[glusterfs:children]
swarm_workers

[glusterfs_master]
docker-worker01
```

# Run-it

```
ansible-playbook setup_ansible/playbook.yml --ask-pass -u root
ansible-playbook update_packages/playbook.yml
ansible-playbook setup_docker/playbook.yml
ansible-playbook setup_dockerswarm/playbook.yml
ansible-playbook setup_glusterfs/playbook.yml
ansible-playbook --limit ansible setup_terraform/playbook.yml
```