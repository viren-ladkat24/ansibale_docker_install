# 🚀 Ansible Multi-Node Automation Project (Nginx + Java + Docker)

## 📌 Overview

This project demonstrates automated infrastructure setup using Ansible with passwordless SSH authentication across multiple nodes.

It includes:

* Web Server → Nginx
* App Server → Java
* Container Setup → Docker

---

##  Architecture

Control Node → Managed Nodes (via SSH)

* Web Server (Nginx)
* App Server (Java + Docker)

---

## ⚙️ Tech Stack

* Ansible
* Linux (Amazon Linux)
* SSH
* Docker

---

## 🔐 Step 1: Passwordless SSH Setup

```bash
ssh-keygen
cat ~/.ssh/id_rsa.pub
```

Paste into:

```bash
~/.ssh/authorized_keys
```

---

## 📂 Inventory File

```ini
[webservers]
web-node ansible_host=172.31.37.25 ansible_user=ec2-user

[appservers]
app-node ansible_host=172.31.35.8 ansible_user=ec2-user
```

---

## ✅ Step 2: Verify Connection

```bash
ansible all -m ping
```

---

## 🌐 Install Nginx (Web Server)

```yaml
- name: Install Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
```

---

## ☕ Install Java (App Server)

```yaml
- name: Install Java
  hosts: appservers
  become: yes

  tasks:
    - name: Install Java
      yum:
        name: java-1.8.0-openjdk
        state: present
```

---

## 🐳 Install Docker (App Server)

```yaml
- name: Install Docker
  hosts: appservers
  become: yes

  tasks:
    - name: Install Docker
      yum:
        name: docker
        state: present

    - name: Start Docker
      service:
        name: docker
        state: started
        enabled: yes
```

---

## ▶️ Run Playbooks

```bash
ansible-playbook install_nginx.yml
ansible-playbook install_java.yml
ansible-playbook install_docker.yml
```

---

## 🔍 Verification

### Nginx:

http://<web-server-ip>

### Java:

```bash
ansible appservers -a "java -version"
```

### Docker:

```bash
ansible appservers -a "docker --version"
```

---

## 💡 Key Concepts

* Ansible Agentless Automation
* SSH Key Authentication
* Multi-node Deployment
* Service Management
* Container Setup with Docker
<img width="1920" height="821" alt="Screenshot (23)" src="https://github.com/user-attachments/assets/0055b771-f67b-425a-9b7d-95fc776f3a66" />

--

---

## 👨‍💻 Author

Viren Ladkat
DevOps Engineer (hands-on projects)
