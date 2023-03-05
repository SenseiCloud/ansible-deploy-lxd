Ansible Deploy LXD

Playbook used to deploy LXD cluster

Don't forget to install community general collection:

```bash
ansible-galaxy collection install community.general
```

## Encrypt vault

To initiate the cluster formation, this playbook uses a token you have to create:

```
# group_vars/all/vault.yml
cluster_password: "SuperPassword"
```

```bash
ansible-vault encrypt group_vars/all/vault.yml
```

## Run the playbook

```bash
ansible-playbook --ask-vault-password -i inventory.ini playbook.yml --extra-vars "lxd_version=latest/stable"
```

## Purge everthing

If you encounter any issues you can purge everyhing using this command:

```bash
ansible all -m shell -i inventory.ini -a "snap remove lxd --purge" --ask-vault-pass
```

## todo

- [x] check for `hostvars[groups['bootstrap']]` instead of direct ansible name