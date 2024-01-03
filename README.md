# Ansible Repository for Class Schedule Project

This repository contains Ansible playbooks, roles, and configurations to manage and deploy various services for the [Class Schedule project](https://github.com/BlueTeam2/ClassSchedule).

## Repository Structure:

- **files:** Contains an initial database dump used to restore the database on the staging env.
- **group_vars:** Contains the `all.yml` file with key variables for different services and configurations. Also includes `service_*.yml`, storing specific service variables.
- **`install_docker` role:** Installs Docker on Ubuntu machines.
- **templates:** Holds Jinja2 templates for application configurations.
- **dynamic inventories:** Includes `production_gcp.yml` and `staging_gcp.yml` for production and stage envs respectively.
- **playbooks:** Docker, Postgres, Tomcat, Grafana, MongoDB, Redis, Node Exporter, and a main playbook orchestrating all.

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

