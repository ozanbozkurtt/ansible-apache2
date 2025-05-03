# Apache Multi-Site Setup with Ansible

This project demonstrates how to automate the installation and configuration of an Apache web server supporting multiple virtual hosts using Ansible.

## 🧩 Overview

With this Ansible role, you can:

- Install and configure Apache
- Define multiple websites with individual virtual host files
- Automatically generate `index.html` for each site
- Enable sites and configure Apache to serve them on port 80
- Add hostnames to `/etc/hosts`
- Validate site availability using HTTP tests (`uri` module)

## 📁 Directory Structure

```bash
.
├── site.yml                   # Main playbook
├── hosts                      # Ansible inventory
└── roles/
    └── apache/
        ├── tasks/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        ├── templates/
        │   ├── apache2.conf.j2
        │   ├── index.html.j2
        │   └── vhost.conf.j2
        └── vars/
            └── main.yml
```

## ⚙️ Prerequisites

- Control Node and Managed Node (Ubuntu 20.04+)
- Ansible installed on the control node
- SSH access between nodes (passwordless recommended)

---

## 📌 Variables

```yaml
apache_package: apache2
apache_service: apache2
server_name: ozan.bozkurt
sites:
  - name: ozan.com
  - name: bozkurt.com
  - name: test.com
```

## 🚀 Usage
### 1. Clone the repository
git clone https://github.com/ozanbozkurtt/ansible-apache2.git

cd ansible-apache-multisite

### 2.Edit the inventory file
```yaml
[webservers]
192.168.1.17 ansible_user=root
```
### 3.Run the playbook

```bash
ansible-playbook -i hosts site.yml
```

## 🧠 Notes
- All virtual hosts are configured to serve over port 80

- Configuration syntax is validated using apachectl configtest

- /etc/hosts is updated dynamically using blockinfile

- Templates allow dynamic site generation and modular structure