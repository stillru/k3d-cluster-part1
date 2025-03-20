# k3d-cluster-part1

This repository contains the code and configurations for **Part 1: Preparations** of the "Home Services Project" article series. Here, I transform an old HP notebook into a home server by setting up a lightweight Kubernetes cluster using [k3d](https://k3d.io/). The goal is to prepare the server for hosting [ScanserverJS](https://sbs20.github.io/scanservjs/) (a scanning service) and [Paperless-NGX](https://docs.paperless-ngx.com/) (a document management solution), all managed via Kubernetes.

## Overview
In this part, I:
- Repurpose an HP notebook as a home server (currently a print/scan station via USB MFU).
- Use Ansible to automate the setup of a k3d cluster—a lightweight Kubernetes environment running in Docker.
- Configure persistent storage with `local-path-provisioner` and automated TLS certificates with `cert-manager` and `step-ca`.

This setup is ideal for learning Kubernetes on limited hardware while preparing for real workloads.

## Repository Contents
- **Ansible Playbooks**: Automate server prep, k3d deployment, and cluster configuration (`playbooks/`).
- **Templates**: Jinja2 templates for k3d config, cert-manager, and step-ca (`templates/`).
- **Variables**: Group and host variables for customization (`group_vars/`, `host_vars/`).
- **Inventory**: Example `inventory.yaml` for Ansible.

Key files:
```
.
├── ansible.cfg
├── group_vars/
│   ├── k3d_servers.yml
│   └── local_servers.yml
├── host_vars/
│   └── k3d.yaml
├── inventory.yaml
├── playbooks/
│   ├── main.yaml
│   └── sections/
│       ├── deploy-certmanager.yaml
│       ├── deploy-helm.yaml
│       ├── deploy-k3d.yaml
│       ├── deploy-local-path.yaml
│       ├── deploy-step-ca.yaml
│       └── prep_server.yaml
└── templates/
    ├── cert-manager.yaml.j2
    ├── clusterissuer.yaml.j2
    ├── k3d-config.yml.j2
    └── smallstep-values.yaml.j2
```

## Prerequisites
- An old computer (e.g., HP notebook) with Linux (Debian/Ubuntu tested).
- Docker installed on the server.
- Ansible installed on your control machine.
- Basic knowledge of Kubernetes, Docker, and Ansible.

## Usage
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/stillru/k3d-cluster-part1.git
   cd k3d-cluster-part1
   ```
2. **Customize Variables**: Edit `group_vars/k3d_servers.yml` and `host_vars/k3d.yaml` with your server details (e.g., hostname, IP).
3. **Update Inventory**: Adjust `inventory.yaml` to point to your server.
4. **Run Ansible**:
   ```bash
   ansible-playbook -i inventory.yaml playbooks/main.yaml
   ```
   This sets up the server, installs k3d, and configures the cluster with storage and certificates.

## What’s Next?
This is Part 1 of a series. In Part 2, I’ll deploy ScanserverJS and Paperless-NGX into this cluster. Check the [full article](https://link-to-your-article) for detailed explanations and diagrams. Stay tuned!

## Contributing
Feel free to fork, tweak, or submit pull requests. Issues and suggestions are welcome!

## License
This project is licensed under the MIT License—see [LICENSE](LICENSE) for details.

---

Happy clustering! Follow my journey on [GitHub](https://github.com/stillru) or connect via [email](mailto:still.ru@gmail.com). Also you can discover my journey in IT at [Personal site](https://stillru.github.io)
