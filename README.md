Proxmox
=========

Installs requirements and interacts with Proxmox server.

Requirements
------------

The following collections are required:

- community.general

They can be installed by running `ansible-galaxy collection install $COLLECTION`.

Role Variables
--------------

See 'defaults/main.yml' or run `grep -E '^[[:alpha:]_]*:' defaults/main.yml| cut -f1 -d:` for plain list.
Details of the variable contents are described [here](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_module.html#parameters).

Example Playbook
----------------

```ansible
- hosts: proxmox

  vars:
    proxmox_api_host: pve-cluster1.example.com
    proxmox_api_user: ansible@pve
    proxmox_api_token_id: ansible
    proxmox_api_token_secret: super-long-secret-goes-here
    proxmox_node: pve1

  tasks:
    - name: Create Ubuntu 22.04 container
      ansible.builtin.import_role:
        role: whalej84.proxmox
	tasks_from: create
      vars:
	proxmox_vmid: 999
	proxmox_ostemplate: local:vztmpl/ubuntu-22.04-standard_22,04-1_amd64.tar.zst

    - name: Delete vmid 999
      ansible.builtin.import_role:
        role: whalej84.proxmox
        tasks_from: delete
      vars:
        proxmox_vmid: 999
	proxmox_purge: true
```
