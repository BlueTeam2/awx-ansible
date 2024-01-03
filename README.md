# Ansible Repository for Class Schedule Project

This repository contains Ansible playbooks, roles, execution-environment and configurations to manage and deploy various services for the [Class Schedule project](https://github.com/BlueTeam2/ClassSchedule).

## Repository Structure:

- **files:** Contains an initial database dump used to restore the database on the staging env.
- **group_vars:** The `all.yml` file includes key variables for various services and configurations, serving as a comprehensive configuration file. Additionally, it encompasses individual `service_*.yml` files, each storing specific service variables tailored for our virtual machines (VMs).
- **host_vars:** The `localhost.yml` file, containing essential variables like gcp_cluster_name, gcp_cluster_zone, az_kubeconfig_path, etc., must be provided for Kubernetes to deploy our application to both the GCP and Azure Kubernetes clusters.
- **cluster-peering role:** Establish a peering connection between different clusters in GCP and Azure using the Mesh Gateways of each cluster.
- **deploy-app-to-kubernetes role:** Deploy our application to Kubernetes Cluster infrastructure.
- **patch-app-vault-secret role:** Updates Kubernetes secrets with data retrieved from Vault.
- **templates:** Holds Jinja2 templates for application configurations.
- **dynamic inventories:** Includes `inventory_dev.yml`, `inventory_stage.yml`, `inventory_prod.yml` and `inventory_global.yml` for development, stage, production and global envs respectively.
- **playbooks:** Cluster Peering, Kubernetes AKS, Kubernetes GCP, Mongo, Nexus, Postgres, Vault, Patch App Secret for AKS/GCP and Patch for Vault secrets. These all playbooks orchestrate `main.yml` playbook.
- **execution-environment:** allows us to deploy all necessary collections, modules, packages and roles for **_Ansible_**

## Usage:

1. **Initial Setup:**
   - Ensure Ansible is installed on your system.
   - Update necessary variables in `group_vars/all.yml` and `group_vars/service_*.yml` files for your specific env configurations.

2. **Deployments:**
   - Use appropriate playbooks with `ansible-playbook <playbook_name.yml>` to deploy services or configure systems. For deploying the entire infrastructure, use `ansible-playbook main.yml`.

3. **Dynamic Inventories:**
   - Utilize `production_gcp.yml` and `staging_gcp.yml` for managing inventory in respective envs.

## Notes:

- Adjust variables in `group_vars` and playbooks based on your env requirements.
- Refer to playbook files for specific configuration details and adjustments.
- Ensure proper access and credentials for connecting to specified envs and services.
- Ensure all machines in your GCP have appropriate labels such as `env:stage|prod` and `app:schedule`.
- Role `install_docker` designed for installing Docker on Ubuntu machines 

