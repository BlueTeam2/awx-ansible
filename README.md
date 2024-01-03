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
- **execution-environment:** allows us to deploy all necessary collections, modules, packages and roles for **_Ansible_**. You can build  the execution-environment Docker image manually with `ansible-builder create` and `ansible-builder build`. By the way you can create AWX job to build image from `execution-environment.yml`.
- **roles/requirements:** AWX automatically installs all the **roles** from `requirements.yml` if it finds such a file. Alternatively, we can manually install roles using the `ansible-galaxy role install -r requirements.yml` command. 

## Usage:

1. **Initial Setup:**
   - Ensure Ansible is installed on your system.
   - Update necessary variables in `group_vars/all.yml` and `group_vars/service_*.yml` files for your specific env configurations.

2. **Deployments:**
   - Use appropriate playbooks with `ansible-playbook <playbook_name.yml>` to deploy services or configure systems. For deploying the entire infrastructure, use `ansible-playbook main.yml`.

3. **Dynamic Inventories:**
   - Utilize `inventory_dev.yml`, `inventory_stage.yml`, `inventory_prod.yml` and `inventory_global.yml` for managing inventory in respective envs.

## Notes:

- Adjust variables in `group_vars` and playbooks based on your env requirements.
- Refer to playbook files for specific configuration details and adjustments.
- Ensure proper access and credentials for connecting to specified envs and services.
- Ensure all machines in your GCP have appropriate labels such as `env:dev|stage|prod|global` and `app:schedule`.
- The `global` environment includes **Vault** and **Nexus** VMs as they are utilized across **dev**, **stage** and **prod** environments. For example, MongoDB is also used in all environments, but its configuration varies for each.
- Role `cluster-peering` designed for peering our Clusters in differents clouds (Azure/GCP).
- Role `deploy-app-to-kubernetes` deploy whole application on our infrastructure.
- Role `patch-app-vault-secret` Updates Kubernetes secrets with data retrieved from Vault.
