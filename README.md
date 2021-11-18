# Ansible Playbooks

A collection of minimalist Ansible playbooks for automating server setups.

- [Initial ansible setup](./setup_ansible): this playbook will prepare your ansible environnements
- [Base system configurations](./setup_base): this playbook will make base system configurations
- [Update system packages](./update_packages/): this playbook will update RHEL & Debian family Linux distros. 
- [Install Docker CE](./setup_docker/): this playbook installs docker-ce
- [Install Docker Swarm](./setup_dockerswarm/): this playbook configure a docker swarm cluster
- [Install GlusterFS](./setup_glusterfs/): this playbook installs and configure a glusterfs cluster (distributed file system)
- [Install Terraform](./setup_terraform/): this playbook installs terraform
- [Install iptables](./setup_iptables/): this playbook activates and configure iptables
- [Install firewalld](./setup_firewalld/): this playbook activates and configure firewalld

# Inventory

Declare all your machines in your hosts files and ansible inventory

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

```bash
[swarm_managers]
docker-manager01

[swarm_workers]
docker-worker01
docker-worker02

[swarm:children]
swarm_managers
swarm_workers

[glusterfs]
docker-manager01
docker-worker01
docker-worker02
```

# Run-it

Run the playbook *setup_ansible* to make ready your server for ansible.

```bash
ansible-playbook --limit "docker-worker01" -u osadmin setup_ansible/playbook.yml 
```

Run this playbook to make the base system configurations

```bash
ansible-playbook --limit "docker-manager01" setup_base/playbook.yml
```

Install docker swarm

```bash
ansible-playbook setup_docker/playbook.yml
ansible-playbook setup_dockerswarm/playbook.yml
ansible-playbook setup_glusterfs/playbook.yml
```

Example to install Terraform only on your ansible machine

```bash
ansible-playbook --limit ansible setup_terraform/playbook.yml
```

# Ops

```bash
ansible all -a "cat /etc/hosts"
ansible all -a "sudo dnf -y install tcpdump"
ansible all -a "systemctl status glusterd"
```