Role Name
=========

This role is patching the vault secrets in kubernetes with new secre-id.

Requirements
------------

This role requires the fully configured kubernetes cluster with the deployed application.

Role Variables
--------------

The role defines variables in `defaults/main.yml`:

### `k8s_kubeconfig_path`

- Path to the Kubernetes config file.
- Default value: `"PATH_TO_KUBECONFIG"`

### `hashicorp_vault_server`

- Address of the HashiCorp Vault server.
- Default value: `"YOUR_HASHICORP_VAULT_SERVER_ADDRESS"`

### `hashicorp_vault_ansible_username`

- Username for Ansible to access HashiCorp Vault.
- Default value: `"YOUR_ANSIBLE_USERNAME"`

### `hashicorp_vault_ansible_password`

- Password for Ansible to access HashiCorp Vault.
- Default value: `"YOUR_ANSIBLE_PASSWORD"`

### `schedule_app_namespace`

- Namespace for your application.
- Default value: `"YOUR_APPLICATION_NAMESPACE"`

### `schedule_app_hashicorp_approle_secret_name`

- Name of the Kubernetes secret storing HashiCorp Vault AppRole credentials for your application.
- Default value: `"YOUR_K8S_APPROLE_SECRET_NAME"`

### `hashicorp_vault_approle_application_secret_id_path`

- Path to the secret ID of the application's AppRole in HashiCorp Vault.
- Default value: `"YOUR_APPROLE_SECRET_PATH"`

Dependencies
------------


This role relies on the `community.hashi_vault`, `kubernetes.core` collections. 

Example Playbook
----------------

```ansible
- name: Patch the kubernetes vault secret
  hosts: localhost
  roles:
    - { 
        role: patch-app-vault-secret,
        k8s_kubeconfig_path: "~/.kube/config" 
    }
```

License
-------

BSD
