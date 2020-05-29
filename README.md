# ar_ssh_config

Create client side ssh config for a set of machines

## Requirements

## Role Variables
The following details:
- the parameters that should be passed to the role (aka vars)
- the defaults that are held
- the secrets that should generally be sourced from an ansible vault.

### Parameters:

Mandatory variables:

| Variable                   | Description                                                              | Default |
| --------                   | -----------                                                              | ------- |
| ar_ssh_config_name         | Name for the SSH config (should be unique across infrastructures)        | None    |
| ar_ssh_config_jump_host    | Jump host (bastion) to use if servers are not directly accessible        | None    |
| ar_ssh_config_machines     | List of machines (see ar_aws_infra->filter_plugins->aws_machine_info.py) | {}      |
| ar_ssh_config_public_user  | User that has access to public machines                                  | None    |
| ar_ssh_config_private_user | User that has access to private machines                                 | None    |


### Defaults
| Variable           | Description                                     | Default                                          |
| --------           | -----------                                     | -------                                          |
| ar_ssh_config_base | Base directory to the client ssh config         | {{ ansible_env.HOME }}/.ssh                      |
| ar_ssh_config_dir  | Directory that will hold extended configuration | config.d                                         |
| ar_ssh_config_path | Path to the extended configuration              | {{ ar_ssh_config_base }}/{{ ar_ssh_config_dir }} |


### Secrets
The following variables should be provided through an encrypted source:

## Example Playbook

```
- hosts: localhost
  tasks:
    - name: Create SSH client config
      include_role:
        name: ar_ssh_config
      vars:
        ar_ssh_config_name: "{{ infra_name }}"
        ar_ssh_config_machines: "{{ ar_aws_infra_all_machines }}"
        ar_ssh_config_public_user: "{{ public_host_user }}"
```
