Role Name
=========

This role deploys the Class Schedule application on single kubernetes cluster.

Requirements
------------
This role requiers the existing kubernetes cluster and preconfigured HashiCorp Vault server. 

Role Variables
--------------

The role defines variables in `defaults/main.yml`:

### `k8s_kubeconfig_path`

- Kubernetes config context path.
- Default value: `$HOME/.kube/config`

### `k8s_repo`

- Git repository URL.
- Default value: `https://github.com/BlueTeam2/class-schedule-k8s.git`

### `k8s_clone_repo`

- Local path for cloning the Kubernetes repository.
- Default value: `/tmp/k8s_class_schedule_chart`

### `schedule_app_namespace`

- Namespace for the schedule app.
- Default value: `schedule-app`

### `schedule_app_backend_name`

- Name of the backend for the schedule app.
- Default value: `backend`

### `schedule_app_backend_image_name`

- Image name for the schedule app backend.
- Default value: `class-schedule-backend`

### `schedule_app_backend_image_tag`

- Tag for the schedule app backend image.
- Default value: `latest`

### `schedule_app_frontend_name`

- Name of the frontend for the schedule app.
- Default value: `frontend`

### `schedule_app_frontend_image_name`

- Image name for the schedule app frontend.
- Default value: `class-schedule-frontend`

### `schedule_app_frontend_image_tag`

- Tag for the schedule app frontend image.
- Default value: `latest`

### `schedule_app_backend_force_update`

- Flag to force update the schedule app backend.
- Default value: `false`

### `schedule_app_frontend_force_update`

- Flag to force update the schedule app frontend.
- Default value: `false`

### `hashicorp_vault_server`

- HashiCorp Vault server URL.
- Default value: `"YOUR_HASHICORP_VAULT_SERVER"`

### `hashicorp_vault_ansible_username`

- Username for accessing HashiCorp Vault via Ansible.
- Default value: `"YOUR_ANSIBLE_USERNAME"`

### `hashicorp_vault_ansible_password`

- Password for accessing HashiCorp Vault via Ansible.
- Default value: `"YOUR_ANSIBLE_PASSWORD"`

### `hashicorp_vault_approle_application_role_id_path`

- Path for the role ID of the application in HashiCorp Vault.
- Default value: `"auth/approle/role/app_{{ app_env }}/role-id"`

### `hashicorp_vault_approle_application_secret_id_path`

- Path for the secret ID of the application in HashiCorp Vault.
- Default value: `"auth/approle/role/app_{{ app_env }}/secret-id"`

### `consul_dc_name`

- Name of the Consul datacenter.
- Default value: `dc1`

Dependencies
------------

This role relies on the `community.hashi_vault`, `kubernetes.core` collections. 

Example Playbook
----------------
```ansible
- name: Deploy schedule application to the kubernetes cluster
  hosts: localhost
  roles:
    - { 
        role: deploy-app-to-kubernetes,
        k8s_kubeconfig_path: "~/.kube/config",
        consul_dc_name: "dc1" 
    }
```

License
-------

BSD
