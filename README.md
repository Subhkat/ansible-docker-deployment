# Ansible Docker Deployment Automation

## Project Overview

This project automates Docker installation and Nginx container deployment on multiple CentOS Stream 9 servers using Ansible.

The playbook performs:

* Docker CE installation
* Docker service configuration
* Python Docker SDK installation
* Nginx image download from Docker Hub
* Nginx container deployment
* Port mapping configuration

---

## Architecture

```text
Ansible Control Node
         |
 -------------------------
 |                       |
Node01               Node02
Docker CE            Docker CE
Nginx Container      Nginx Container
```

---

## Environment

| Component | Details                          |
| --------- | -------------------------------- |
| OS        | CentOS Stream 9                  |
| Ansible   | 2.14                             |
| Docker    | Docker CE                        |
| Container | Nginx                            |
| Nodes     | 1 Control Node + 2 Managed Nodes |

---

## Project Structure

```text
ansible-docker-deployment/
├── ansible.cfg
├── inventory
│   └── hosts
├── playbook
│   └── site.yml
├── README.md
└── roles
    └── docker
        ├── tasks
        │   └── main.yml
        ├── vars
        │   └── main.yml
        ├── handlers
        ├── templates
        ├── defaults
        └── files
```

---

## Inventory Configuration

File:

```bash
inventory/hosts
```

```ini
[docker]
192.168.0.10
192.168.0.11
```

---

## Ansible Configuration

File:

```bash
ansible.cfg
```

```ini
[defaults]
inventory=inventory/hosts
roles_path=roles
host_key_checking=False
remote_user=root
```

---

## Verify Connectivity

```bash
ansible all -m ping
```

---

## Syntax Check

```bash
ansible-playbook playbook/site.yml --syntax-check
```

---

## Run Playbook

```bash
ansible-playbook playbook/site.yml
```

---

## Verification

Check Docker service:

```bash
systemctl status docker
```

Check containers:

```bash
docker ps
```

Check images:

```bash
docker images
```

Check Nginx:

```bash
curl http://localhost:8080
```

Expected output:

```html
Welcome to nginx!
```

---

## Troubleshooting

### Docker Service Not Found

Issue:

```text
Could not find the requested service docker
```

Resolution:

Install Docker CE repository and Docker CE packages instead of the default podman-docker package.

---

### Python Docker SDK Error

Issue:

```text
No module named pkg_resources
```

Resolution:

```bash
dnf install python3-setuptools -y
```

---

### Variable Not Defined

Issue:

```text
'omage_name' is undefined
```

Resolution:

Correct variable name:

```yaml
image_name
```

---

## Skills Demonstrated

* Ansible Roles
* Inventory Management
* Variables
* Docker CE Installation
* Container Deployment
* YAML Troubleshooting
* Linux Administration
* Git & GitHub

---

## Author

Subhash Waghela
Linux System Engineer
