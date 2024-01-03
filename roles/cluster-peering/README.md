Role Name
=========

A brief description of the role goes here.

Requirements
------------

This role requieres the fully configured kubernetes cluster with the deployed consul.

Role Variables
--------------

The role defines variables in `defaults/main.yml`:

### `consul_namespace`

- Namespace for Consul.
- Default value: `consul`

### `peering_acceptor_dc_name`

- Datacenter name for the peering acceptor.
- Default value: `gcp`

### `peering_acceptor_kubeconfig_path`

- Path to the kubeconfig file for the peering acceptor.
- Default value: `""`

### `peering_dialer_dc_name`

- Datacenter name for the peering dialer.
- Default value: `azure`

### `peering_dialer_kubeconfig_path`

- Path to the kubeconfig file for the peering dialer.
- Default value: `""` (empty string)


Dependencies
------------

This role relies on the `community.hashi_vault`, `kubernetes.core` collections. 

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- name: Configure consul cluster peering
  hosts: localhost
  roles:
    - { 
      role: cluster-peering, 
      peering_acceptor_dc_name: "dc1",
      peering_acceptor_kubeconfig_path: "~/.kube/config_dc1" ,
      peering_dialer_dc_name: "dc2",
      peering_dialer_kubeconfig_path: "~/.kube/config_dc2" 
    }

```
License
-------

BSD
